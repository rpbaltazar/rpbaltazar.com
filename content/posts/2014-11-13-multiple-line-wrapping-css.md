---
author: rpbaltazar
categories:
- Software development
date: "2014-11-13T02:52:00Z"
guid: http://balazar.net/random/?p=98
id: 98
tags:
- css
- html
- line-wrapping
- overflow
title: Multiple line wrapping CSS
url: /2014/11/13/multiple-line-wrapping-css/
videourl:
- ""
---
Recently in our project we&#8217;ve had an issue that involved multiline text wrapping. It&#8217;s always been a bit shaddy to do it. Some people use character count and then chop the string, some others just rely on the height and so on.

The inexistence of a overall accepted answer worries me a little bit, given that it is not so uncommon.
I understand that, with the mobile invasion of the market, mobile first and changing the website to show contents according to which platform you are using makes total sense, and wrapping with ellipsis shouldn&#8217;t be the solution.

Hiding content from the users is never the solution, showing a bit and tell them &#8220;Ah! Ah! you can&#8217;t see more!!&#8221; is even worse! Nevertheless, in this specific scenario, wrapping with ellipsis is accepted provided that we can have multiple line.

Luckily for us, we are developing solely for google chrome, and we have webkit available, so here is the solution we&#8217;ve adopted.

  * <a href="https://gist.github.com/rpbaltazar/069bc1a1e81ebe9b8eb7" title="Gist" target="_blank">Gist</a>
  * <a href="http://jsfiddle.net/rpbaltazar/q9uhojps/1/" title="jsFiddle" target="_blank">jsFiddle</a>

Enjoy
