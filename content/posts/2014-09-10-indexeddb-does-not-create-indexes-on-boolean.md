---
author: rpbaltazar
categories:
- Curiosities
- Databases
- Software development
date: "2014-09-10T07:04:14Z"
tags:
- indexeddb
- javascript
- js
title: IndexedDB does not create indexes on boolean
---
In my current job, we are using indexedDB to handle data offline and make it available on the browser even when there is no internet connection.

Recently, one of the tasks that we had made us think that would be useful to create an index with an id attribute and a boolean. The idea behind this was to filter the dataset returned by the indexedDB and avoid having to filter it.

Turns out, indexedDB does not create indexes over boolean values. If we reason it, booleans are actually a low cardinality field, therefore does not make much sense to create an index for a boolean column.
On the other side, using the boolean with something else, seems reasonable and useful for me.

We ended up by fetching all the results (filtered only by the attribute id) and then ignore the ones that have the boolean set to false. One other possible solution would be converting true/false to 1/0 but that doesn't seem feasible in a real product situation.

In conclusion:

* IndexedDB does not create indexes for booleans columns
* If you try to create, it will appear on your list of indexes, but it won't be filled at all
* If you try to access it, you'll have an error thrown
