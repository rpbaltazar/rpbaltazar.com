---
author: rpbaltazar
categories:
- Productivity Tools
- Tracker Tools
- Ruby Gem
date: "2019-10-29T00:00:00Z"
tags:
- tools
title: Story Branch - Branch utility gem
---

Something that bugs me a lot, particularly when I'm working with other people
in the same project are meaningless branch names. This leads to confusion and
sometimes conflicting names. Thus, I would like to write about this gem I've been
developing and maintaining for quite some time - [StoryBranch](https://github.com/story-branch/story_branch).

## Some Background

The development of this gem has started quite some time ago as an internal tool
to integrate with the tracker we were using in my company - PivotalTracker.
Some of the commands available still connect directly to that tracker, but I've
put a significant amount of time refactoring the code, cleaning it up and make
it more modular. At the moment it has integration with Github (which I use for
tracking the issues for the Gem), PivotalTracker (which I currently don't use
but should still be fully functional) and recently initial integration with
JIRA (which I currently use in my company).

## Use case

As I've mentioned in the beginning of the article, I'm somewhat picky about
branch names and how each one of them, while they live, they mean something.
Even more, if I can directly from the branch name, pinpoint the issue that I'm
trying to solve.
With this gem, once configured with your project, just by running
`story_branch create` it'll look for issues in the configured tracker, list them
for you to choose one from and create the branch from the issue name and id.

I reckon that there are different workflows for different companies and trackers
and a lot of the refactoring I've been doing is with that in mind. My view for
this project is that I'd provide a basic workflow integration with the different
trackers but allow it to be extendable so each project could have its own.

## Conclusion

I'm all in favor of tools that make me more efficient and clear with my work,
and this is one of my go to tools. Give it a try and you'll certainly see the
benefits of it. Feel free to give feedback in the gem repo itself or suggestions
on how to make it better for your use case.
