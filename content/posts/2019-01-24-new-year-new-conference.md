---
author: rpbaltazar
categories:
- Conferences
- Ruby
date: "2019-01-24T00:00:00Z"
tags:
- RubyConfIndia
title: New Year, New Conference
---
## The outcome of Ruby Conf India 2019

As part of my 2019 resolutions I’ve decided that I should write more often. I’ve attended plenty of talks where the presenter states that writing often actually helps you grow, so this year I’ve decided to take the leap.

Thanks to the company I work for, [OpsManager](https://opsmanager.com), I got the chance to attend the [Ruby Conf India](https://www.rubyconfindia.org/), this last weekend and why not starting my new goal by writing a small summary of what I’ve found interesting during these two days of talks.

![OpsManager team with Matz](https://cdn-images-1.medium.com/max/8064/1*AuOTaFj3jAWeK6nCqoyWbw.jpeg)*OpsManager team with Matz*


### Notes on Matz's talk

The conference started with an opening keynote by a regular starter — Matz. In this presentation, unlike others by Matz that I have attended, a few things stroke me. First is that we are walking fast towards the retirement of THE man behind ruby and this is raising quite a few questions on the core team. Who and how are they going to replace Matz who has always had a strong opinion in regards to ruby development. I’m pretty sure they will find a solution, but there might be a critical transition period, that hopefully will run as smoothly as the latest ruby releases upgrades! On other notes, Matz mentioned that this year will be the year of the concurrency for him and how ruby 3 is planned to bring better tooling. Finally he re-stated that static typing in ruby is something that should not be needed and he won’t do any work towards that direction.

### Notes on Brad Urani's talk

[Brad Urani](http://fractalbanana.com) brought in some interesting tips on how to build a better command line shell. In my case, I already use most of the suggestions but he did mention something I’m planning to try which is the combo [awesome_print gem](https://github.com/awesome-print/awesome_print) and [pry](https://github.com/pry/pry).
He also had a funny quote (or at least for VIM users): The VIM usage and pregnancy follow the same pattern:

1. Suffering

1. Stockholm Syndrom

1. Sunk cost fallacy

> # *If Ruby is the language, Rails is the joke told in that language*

I don’t particularly share the “hate” (hate is a very strong word and I’d like to use something more mild) that I’ve seen recently towards Rails but I still found the quote funny. Also, a side note is that I think a lot of the developers complaining about Rails and doing nothing to change it are not only part of the problem but also forget that some of them actually have a job because of Rails.

This conference had a rather interesting approach. I had the impression that they didn’t have enough speakers so they smartly restructured the conference and added an 1 hour around the table for free topic discussion. Things went pretty smoothly and the discussion flown in most groups. The group I was discussing at was talking about Machine Learning in Ruby. I haven’t yet explored much about machine learning but I did learn that there are some efforts to develop some kind of framework for Machine Learning in Ruby. [Daru](https://github.com/SciRuby/daru) is out there and is the beginning of it, and from the POV of some data scientist, what is missing now is a simple Machine Learning Library but most important a consistent and stable API. If you are interested in this topic, you might want to have a quick chat with the [Daru](https://github.com/SciRuby/daru) fellows or [Soumendra](https://twitter.com/dataBiryani).

### Notes on Charles Nutter's talk

Moving on, JRuby made a major appearance in this weekend’s conference. [Charles Nutter](https://twitter.com/headius) came all the way to tell us that JRuby is starting to be blazing fast including in Rails applications. They are very open to support in the migration and wanting badly help from people testing all the tiny little details.
Speaking of tiny little details, JRuby is now compatible about 99% with Rails applications. So if you do have a rails application, give it a go. Take here a look at the performance graphs.


### Notes on Jason Swett's talk

One of the last talks of the last day was done by [Jason Swett](https://www.codewithjason.com/) and he spoke about working with legacy code and in particular lagacy code that does not have test coverage. Nowadays everyone understands (hopefully) the importance of testing, but that was not the case in many of the existing applications in production. Jason brought to the table 3 different techniques, inspired by [Michael Feathers book](https://www.amazon.com/Working-Effectively-Legacy-Michael-Feathers/dp/0131177052) on how to start building a test suite for a legacy codebase that does not have one. Doing such exercise will not only improve the stability of the code as you’re more prone to find the bugs but will also help you to understand better the codebase you’re working with.
The three suggested approaches are:

1. Sprout method — Move a chunk of code to a new method that allows it to be more easily tested
1. Sprout class — Move a chunk of code to a new class again making it more decoupled and more easily testable.
1. Characterization testing (or reverse TDD)
  * Comment an entire class
  * Write a failing test for the first line of code
  * Uncomment the code
  * Expect it to pass

One more tip that Jason gave is that when writing tests for existing code without tests, focus on easiest first.

### Notes on GoJek's talk

And to finalize my summary (and this very long post), [GoJek](https://gojek.com) gave a very interesting talk on how they monitor their large scale applications. They have built their own pipeline of logging and collecting those logs making use of a series of different open source projects. Because they have a large amount of data being generated, all stored data is downsampled. According to the talk, monitoring involves 3 main steps:

1. Report and aggregate
1. Store the data
1. Visualize

For each one of these steps, they introduced one solution:
For Reporting, they chose to use [statsd-ruby](https://github.com/github/statsd-ruby). The Aggregation step is taken care by [telegraf](https://portal.influxdata.com/downloads/) which is characterized by low memory footprint and a series of ready to use built in plugins. For data storing, they rely on the [influxdb](https://portal.influxdata.com/downloads/) and finally, for data visualization they rely on [grafana](https://grafana.com/get).

From here, I deduced that we can probably achieve something similar by logging application specific events and relying on Scout to collect and aggregate them, which we shall try later on this month.
