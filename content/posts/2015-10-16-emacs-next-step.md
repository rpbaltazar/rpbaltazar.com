---
author: rpbaltazar
categories:
- Curiosities
- OSx
date: "2015-10-16T02:34:18Z"
tags:
- emacs
- osx
- text editor
title: Emacs, next step
---
Once I've gotten familiar with the basic commands, my first problem was how ugly emacs looked out of the box. No one on earth can have any pleasure working on an ugly UI.
So I've started looking for how to change it.

This lead me to the initialization of configuring emacs defaults.

<!--more-->

**Customizing**:

First thing, assuming that you're going all in with the emacs (or vim) they heavily rely on keystrokes instead of mouse moving. So let's remove the ugly toolbar from the top of the window:

```
M-x tool-bar-mode
```

And done. Its gone. This is nice but, you don't want to type it everytime you start emacs. So we need to make sure this is executed on initialization.
By default, Emacs looks for .emacs file in your home folder. In case it does not find such file, it'll look for a folder called .emacs.d and inside it look for a file called init.el.

As you can imagine, we'll go ahead with the folder creation because you can already expect a lot of configurations coming up.
In your init.el file, write:

```
(tool-bar-mode -1)
```

If you close your emacs and open it again, you shouldn't see anymore the toolbar.
Now let's make the colorscheme a bit more friendly.
There are a bunch of pre-installed colorschemes that you can choose from or you can install a new one.

Lets choose an existing one for now. If you type:

```
M-x load-theme
```

You can use Tab to see available themes. I started with 'misterioso'.
Similarly to the toolbar, you don't want to set a theme everytime you start emacs. So, add it to your init file

```
(load-theme 'misterioso)
```

Save the file, close and open emacs and you should see emacs with your new theme.

Next entry I'll be explaining my baby steps on package management and which packages I've installed right away...
