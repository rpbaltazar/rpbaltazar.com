---
author: rpbaltazar
categories:
- Blogging
date: "2013-10-25T02:54:21Z"
guid: http://balazar.net/random/?p=40
id: 40
tags:
- html
- indentation
- wordpress
title: Worpress indent text
url: /2013/10/25/worpress-indent-text/
---
The problem:
I have a piece of code that I want to show indented, but adding blank spaces by pressing the space bar is not solving the issue.

Also, using &#8220;&nbsp;&#8221; will disappear if I jump from Visual to Text mode.

The solution:

  * <pre>Use this html trick: &lt;span style="visibility: hidden;"&gt;+++&lt;/span&gt;</pre>

    The number of characters give you the indentation. The character used is not important.</li>

      * <pre>Single line indentation is also possible by using the following: &lt;span style="margin-left:28px;"&gt;Start writing here&lt;/span&gt;</pre></ul>

    <a href="http://wpbtips.wordpress.com/2009/06/19/formatting-text-pt-2/" target="_blank">Full reference</a>
