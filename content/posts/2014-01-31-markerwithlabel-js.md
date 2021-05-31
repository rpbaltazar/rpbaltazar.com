---
author: rpbaltazar
categories:
- Computer Science
- Curiosities
date: "2014-01-31T07:55:32Z"
guid: http://balazar.net/random/?p=73
id: 73
tags:
- google maps
- javascript
- js
- library
- maps
- markers
- markerwithlabel
- web
title: MarkerWithLabel.js
url: /2014/01/31/markerwithlabel-js/
---
I&#8217;ve been using the lib MarkerWithLabel by Gary Little, available in <a title="here" href="http://google-maps-utility-library-v3.googlecode.com/svn/tags/markerwithlabel/1.1.9/src/markerwithlabel.js" target="_blank">here</a> (check for the most recent version) and recently had a problem that took me a bit to figure out: How to update the label without having to remove the marker from the map and put it back again.

Therefore, I&#8217;ve made a few google queries and here is what i found to be the best solution:

<pre>marker.labelContent = ""+(index+1);
marker.label.draw();
</pre>
