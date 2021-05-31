---
author: rpbaltazar
categories:
- Curiosities
- OSx
date: "2015-10-16T02:34:18Z"
guid: http://balazar.net/random/?p=144
id: 144
image: /wp-content/uploads/2015/10/cartoon94.png
tags:
- emacs
- osx
- text editor
title: Emacs, next step
url: /2015/10/16/emacs-next-step/
---
Once I&#8217;ve gotten familiar wiht the basic commands, my first problem was how ugly emacs looked out of the box. No one on earth can have any pleasure working on an ugly UI.
So I&#8217;ve started looking for how to change it.

This lead me to the initialization of configuring emacs defaults.

<!--more-->

**Customizing**:

First thing, assuming that you&#8217;re going all in with the emacs (or vim) they heavily rely on keystrokes instead of mouse moving. So let&#8217;s remove the ugly toolbar from the top of the window:

`<br />
M-x tool-bar-mode<br />
`

And done. Its gone. This is nice but, you don&#8217;t want to type it everytime you start emacs. So we need to make sure this is executed on initialization.
By default, Emacs looks for .emacs file in your home folder. In case it does not find such file, it&#8217;ll look for a folder called .emacs.d and inside it look for a file called init.el.

As you can imagine, we&#8217;ll go ahead with the folder creation because you can already expect a lot of configurations coming up.
In your init.el file, write:

`<br />
(tool-bar-mode -1)<br />
`

If you close your emacs and open it again, you shouldn&#8217;t see anymore the toolbar.
Now let&#8217;s make the colorscheme a bit more friendly.
There are a bunch of pre-installed colorschemes that you can choose from or you can install a new one.

Lets choose an existing one for now. If you type:

`<br />
M-x load-theme<br />
`

You can use Tab to see available themes. I started with &#8216;misterioso&#8217;.
Similarly to the toolbar, you don&#8217;t want to set a theme everytime you start emacs. So, add it to your init file

`<br />
(load-theme 'misterioso)<br />
`

Save the file, close and open emacs and you should see emacs with your new theme.

Next entry I&#8217;ll be explaining my baby steps on package management and which packages I&#8217;ve installed right away&#8230;
