---
author: rpbaltazar
categories:
- Curiosities
- Terminal
date: "2015-06-22T02:35:47Z"
tags:
- delete files
- find
- terminal
- unix
title: Find and delete files in a tree
---
Recently I found that our current project had a bunch of temporary files that were not being cleaned up.
They are created by Emacs and not cleaned up, probably due to not closing the buffers properly.

As they were a bunch of them, I didn't feel like doing one by one and they all matched a certain pattern:
```
/#filename#
```

So, to delete them, I've used find with args regex and delete.
Might become handy sometime in the future.

```
find . -regex '.*\#.*\#$' -delete
```

This command would translate to
```
find recursively from current directory files matching the regex ".*\#.*\#$" and delete them.
```

Another interesting note on find is that it returns the path from the passed directory (in our case, current directory), therefore, for the regex to match, we are accepting any character any amount of times as long as the filename ends with
```
/#filename#
```

Finally, in case you're wondering, $ means end of string so we ensure there is nothing after the desired pattern.
