---
author: rpbaltazar
categories:
- Software development
date: "2014-06-30T10:30:59Z"
guid: http://balazar.net/random/?p=85
id: 85
image: /wp-content/uploads/2014/06/man-1191845_1280.jpg
tags:
- guidelines
- project management
- web
title: Starting a new project? Some guidelines
url: /2014/06/30/starting-a-new-project-some-guidelines/
---
When starting a new project is important for you to keep in mind that it is going to be used and handled by someone else in the future (worst case scenario is the future you &#8211; who might not remember everything your present you thought when starting the project). Therefore, there are some basic steps that you can go through in order to keep your project organised, usable and maintainable.
<!--more-->

  * Write a README file
  * Write an meaningful introduction
  * List your dependencies
  * Explain how to setup the local development environment
  * Which environment variables you need to configure
  * How to deploy

  * Use a source version control such as GIT
  * Keep your master branch always deployable
  * Write meaningful commit messages
  * If working in a team, consider using pull requests and code review

  * Highly recommend to use environment variables to store configuration params
  * Use package managers (when possible)
  * Automate your deploy procedure
  * Make your application work in different environments, usually:
  * development
  * test
  * staging
  * production

  * Consider using CDN to serve static files
  * DO write tests to cover your features*

The original post came from: http://blog.arvidandersson.se/2014/06/17/best-practices-in-modern-web-projects.

*Added by me as per my experience working in TDD environments and not
