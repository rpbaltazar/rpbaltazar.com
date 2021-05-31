---
author: rpbaltazar
categories:
- Computer Science
- Databases
- Rails 6
date: "2020-05-19T00:00:00Z"
tags:
- databases
- postgresql
- rails
- sql
- fail
title: Read/Write replicas in Rails 6
---
This will be part 1 of a series where I'll describe my adventures on getting Rails 6 to query read
replicas successfully in real life application.
If you have read the blog posts about how Rails 6 introduced replicas capabilities most of them make you feel like it is just plug and play. In reality, that is not the case and development based on your application context will need to be done. As you'd suspect, in any core development around the database it is highly connected to your application and business logic so coming up with a generic solution is very unlikely.

## What does Rails 6 have?

What Rails 6 provides you out of the box is not a production ready solution for read write replicas (nor they advertise that) but a core to support it with a [very lightweight example](https://guides.rubyonrails.org/active_record_multiple_databases.html) of how to do it. What most articles do is they expand lightly the contents of Rails team explanation but they don't highlight some of the issues you might find and you should be aware of. The given solution works perfectly fine in a development environment, probably even on a staging/testing environment but its when it hits the production with high concurrency and multiple servers that the issues start to be clear.

## What have I found so far - AKA what has bitten me

### Business logic caveat

As I mentioned in the introduction, this kind of work is highly dependent on your implementation and business logic. The first problems that were nearly immediately spotted (some caught by our tests, some others gave us the opportunity to improve our test coverage) were caused by GET requests that would actually need a write connection. We didn't have many of these cases but in such cases I had to come up with a solution for it as well. In this case, what I initially did to solve the problem was to request a new connection to the primary database with write permissions. I read in the rails commits that this solution is actually discouraged and [is already deprecated on master](https://github.com/rails/rails/pull/37874) it since our problems were deeper than this, I'm actually testing another approach now. This new approach is meant to sit on the middleware level and be transparent on the controller so no context switching in the middle of the request.

### Rails guarantees "read your own write" caveat

> Rails guarantees "read your own write" and will send your GET or HEAD request to the primary if it's within the delay window. By default the delay is set to 2 seconds. You should change this based on your database infrastructure. Rails doesn't guarantee "read a recent write" for other users within the delay window and will send GET and HEAD requests to the replicas unless they wrote recently.

Initially this read to me as in the Rails team had an internal way of determining if the same request originator was trying to read a recently written record and if that was the case, they would assign a write connection (provided it was within the 2 second delay). Turns out it is not that straightforward if you are running an API only rails application. You can see how the internals work for [determining if there was a recent write](https://github.com/rails/rails/blob/62e05ce/activerecord/lib/active_record/middleware/database_selector/resolver.rb#L77-L87) and how to [update the recent write timestamp](https://github.com/rails/rails/blob/62e05ce96f771f2a292ad1ce87faaac1a1d886c7/activerecord/lib/active_record/middleware/database_selector/resolver/session.rb#L38-L40). This relies on the session information which (unless you've explicitly configured that way) is not available in a rails api only application.

The way this bit me was that even though we have a significantly low read replica latency some of our api consumers actually manage to make subsequent requests faster than the replica being available and they wouldn't find the record they had just created. This was particularly critical in our case because one of the records was the authentication token. This happen only in production because of the load distribution. The token creation was being sent to a pod A and the next request sent to pod B. Pod A would update its recent write information while pod B wouldn't know anything about it so it would fail to authenticate the request.

This was the by far the hardest problem to spot because we only saw it coming when already in production and we had an increase of unauthenticated requests.

## Wrap up

  1. Most of Rails 6 Write/Read replica articles do not talk about potential issues which leads me to think that they only replicated the rails 6 article.
  1. You'll need to adjust your read from replica logic based on your business logic. An out of the box solution is very unlikely to fit all.
  1. If you're doing pure CRUD and using rails sessions you'll probably be fine with Rails 6 provided solution. Unfortunately that is not the case for most large applications.
  1. When testing try to identify your production use cases and test them. If you are an running an API application try to understand your clients patterns on API consumption and test their workflows. Ensuring an API endpoint works won't suffice when dealing with these changes.
