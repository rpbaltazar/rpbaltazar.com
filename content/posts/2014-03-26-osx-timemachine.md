---
author: rpbaltazar
categories:
- Curiosities
- OSx
date: "2014-03-26T19:38:47Z"
guid: http://balazar.net/random/?p=77
id: 77
tags:
- backup
- mavericks
- osx
- time machine
title: OSx TimeMachine
url: /2014/03/26/osx-timemachine/
---
I&#8217;ve been using Apple&#8217;s TimeMachine to perform my computer&#8217;s backup. This has proven to be working and I have no complaints so far. Initially, I&#8217;d created a disk partition of 600GB to keep the backup of my tiny 256GB disk. It has been working good since September, but recently I&#8217;ve started running out of space. Given that September 2013 seems a too recent past for me, I&#8217;ve decided to buy a larger disk to perform the backups.

My new 2TB disk arrived, wiped the usual disk contents using the recommended format for TimeMachine (Mac OS Extended, case-sensitive, journaled) and tried to copy the backups from the old disk to the new, following [Apple&#8217;s instructions](http://support.apple.com/kb/ht5096). After 5 minutes indexing files and preparing to copy, an error message started to pop up. Actually, a couple of alerts popped up:

> Error 1: &#8220;&#8221; cannot be converted. Please install a newer version of iWork.
> Error 2: The operation can&#8217;t be completed because you don&#8217;t have permission to access some of the items.
> Error 3: The operation can&#8217;t be completed because an unexpected error occurred (error code -8062).
> Error 4: The operation can&#8217;t be completed because you don&#8217;t have permission to access some of the items.
> Error 5: The operation can&#8217;t be completed because you don&#8217;t have permission to access some of the items.

And this hanged the copy of the backups from one side to the other.

So with a bit of googling, managed to find another proposed solution, which seems to be working.
Instead of using Finder, I used the Disk Utility. It has an option called restore, that allows the users to copy the contents of one disk (or image) to another disk.
Very simple to use, this tool managed to copy everything from my original disk to the new one and save me from a lot of trouble.

I hope.
