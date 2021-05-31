---
author: rpbaltazar
categories:
- Databases
- RoR
- Software development
date: "2015-04-29T08:15:28Z"
guid: http://balazar.net/random/?p=118
id: 118
tags:
- Database
- performance
- rails
- rails 4
- ror
- sql
- web
title: Bullet Gem
url: /2015/04/29/bullet-gem/
---
Recently in one of our projects, we decided to take a deeper look at N+1 queries, as well as general DB Operations performance. We&#8217;ve started by installing [this awesome gem called bullet](https://github.com/flyerhzm/bullet) .
This gem, creates a log file for you, where it lists all the N+1 queries found, unnecessary eager loading queries and missing requires. This is quite useful as a starting point for improving your general web application performance.

We&#8217;ve successfully cleaned up most of the logged queries and we&#8217;ve moved on with our lives.
Because our application relies a lot on indexedDB, we&#8217;ve never experienced (at least not until today) a lot of hassle after making bullet part of our development environment.
<!--more-->

Today we were puzzled by where the heck the application was losing so much time and taking so long to answer to the client side, even after rails logging
`Completed 200 OK in 551ms (Views: 170.3ms | ActiveRecord: 37.0ms)`
By a lot of time, we&#8217;re talking about 50 seconds until [TTFB](http://en.wikipedia.org/wiki/Time_To_First_Byte).

After a lot of head banging against the wall, we&#8217;ve decided to move bullet away from our dev environment and&#8230;. boom! Performance back to normal.

Lesson learnt: &#8220;If you plan to use bullet, use it while you need it and then put it away. It will bite your ass when you least expect&#8221;.
