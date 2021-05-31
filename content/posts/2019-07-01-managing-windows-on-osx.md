---
author: rpbaltazar
categories:
- Productivity Tools
- Computer Configuration
date: "2019-07-01T00:00:00Z"
tags:
- tools
title: Managing windows on OS X
---

It's been a while that I'm a particular fan of using mostly my keyboard as navigation tool in the computer.
I try to avoid the use of the mouse for almost everything I do on my daily basis, except browsing the
internet. I'm still a bit far from that Geekiness level. In this blog post I'll talk about two levels of
customization: Text editor and Window manager.

## Text Editor - VSCode

I don't want to start the discussion of which text editor is the best and which one provides the best
tool for the job, ... In my opinion, when it comes to text editors, the best tool for the job is the
one that you are able to be the most productive with while being able to customize it to your taste
without wasting precious time. I've started as [MacVim](https://github.com/macvim-dev/macvim) user,
moved to Emacs, tried Atom and for now I'm settled with VSCode. Aside from [Atom](https://github.com/atom/atom/)
that I've stopped using because the search for text in the project would
[kill my machine](https://github.com/atom/atom/issues/16692), I've stopped using both VIM and Emacs
for different reasons at the time but I believe that it all boiled down to never feeling
like a power user in any of them. There are tons of plugins available for both and this includes
multiple ways of managing and installing them, which is good once you know what you want but bad
when you are in the discovery phase. I believe that VSCode made a good job in containing the plugin
ecosystem. Nothing stops you from installing random plugins, but generally the plugin management
is done through the "extension market place".

### Screen splitting

Back to the focus of the article, two things that I got used to while using other text editors that
are absolute essential for me are vertical and horizontal splitting of the text editor, where I can
have multiple tabs open. I use them often enough for missing them when I don't have it.
For example, when I'm working on a subclass and I need to refer back to the superclass, I like to
have two tabs open with the two classes. Similarly, when I'm working on some piece of code, I often
like to have the matching unit test files open. And for this, I usually use the vertical split of the
text editor.

That being said, I know that the latest default configuration of VSCode allows splitting horizontally with
`cmd+<number>`, where number should match an existing split or the highest after the ones you have
opened at the moment, but for me, I generally prefer to use `cmd+k <arrow>` to split the editor.

### Navigating between splits

Once I have a couple of files open, I tend to need to switch between the splits. For that, I rely on
another configured shortcut `ctrl-w`

### Text navigation

Because of my habits from Emacs and terminal, navigating through the text itself, I rely on
`alt+g alt+g` to trigger the go to line.

Though personally I still prefer to use the terminal app itself, sometimes I do use the in-built
terminal option. For toggling between the text editor and the terminal I've set ``ctrl-` ``

For beginning and end of lines I use `ctrl+a` and `ctrl-e`
as one would use in the terminal. There are quite a few more shortcuts that I rely on but most of
them are standard out of the box options, such us vertical select (`alt+cmd+<up/down>`),
multi-word select (`cmd+d`).

### Conclusion

In sort of a summary, the idea is that you should learn which are the steps that you
repeat more often while coding, particularly those that require you to use the mouse.
Some common things I see in my day to day are:

1. Creating and deleting files in the tree;
2. Looking for a particular file;
3. Switching between tabs or files;

And these operations can definitely be optimized for your best comfort.

## Window Manager

As for the actual screen management, and different application window sizing,
placement and navigation, I also have a tool of choice. In my case, because I've
been working with OSx most of my developer time, I'm used to use [Phoenix](https://github.com/kasper/phoenix).
This lightweight application allows you to build your own window management configuration
using Javascript. It basically provides you with an api for managing your windows
and allows you to configure keyboard shortcuts for each of the actions you use more
frequently.

My [personal configuration](https://github.com/rpbaltazar/phoenix-config) has a lot of shortcuts but
the ones I use the most are:

1. Moving a window to the other screen - This one is particularly useful when I'm
at work with my 2 screen setup;
2. Resizing and placing a window in one of the quarters of the screen;
3. Resizing and placing a window in half of the screen;
4. Resizing and placing a window in a customizable grid;
5. Full screen a window;

In Phoenix repository there are a bunch of configuration demos and I highly recommend you to take
a look at them and give this a try. If you're not yet using the power of keyboard shortcuts you're
missing out.
