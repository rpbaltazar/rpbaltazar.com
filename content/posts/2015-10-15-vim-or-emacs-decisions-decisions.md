---
author: rpbaltazar
categories:
- OSx
date: "2015-10-15T10:19:20Z"
tags:
- emacs
- mac
- text editor
- vim
title: Vim or Emacs... decisions decisions...
---
This will be a part of a series where I'll be trying the devil's question. Vim, or Emacs.
I do understand that for taking a real big advantage from any of both, you should be a long-term user, as it implies a lot of configuration and it takes a lot of personal taste.

Nevertheless, let the journey begin...

I'm currently using a Macbook Air with Yosemite in it.

Emacs... let's do it.

  1. Installation
    ```
      brew install emacs --HEAD --use-git-head --with-cocoa --srgb
    ```

  2. If you didn't link emacs app to your applications folder, I'd suggest you to do so.
    ```
      brew linkapps emacs
    ```

  3. Once you start emacs, you can close it by pressing:
    ```
      C-x C-c
    ```
    Please note that C means Control

  * Keyboard basics

  | Key combination | Action                 |
  | --------------- | ---------------------- |
  | C-p             | Up one line            |
  | C-n             | Down one line          |
  | C-f             | Forward one character  |
  | C-b             | Backward one character |
  | C-a             | Beginning of line      |
  | C-e             | End of line            |
  | C-v             | Down one page          |
  | M-v             | Up one page            |
  | M-f             | Forward one word       |
  | M-b             | Backward one word      |
  | M-<             | Beginning of buffer    |
  | M->             | End of buffer          |
  | C-g             | Quit current operation |

  * Basic functions and their shortcuts

  | Key combination | Function           | Description                        |
  | --------------- | ------------------ | ---------------------------------- |
  | C-x C-s         | save-buffer        | Save the current buffer to disk    |
  | C-x u           | undo               | Undo the last operation            |
  | C-x C-f         | find-file          | Open a file from disk              |
  | C-s             | isearch-forward    | Search forward for a string        |
  | C-r             | isearch-backward   | Search backward for a string       |
  |                 | replace-string     | Search & replace for a string      |
  |                 | replace-regexp     | Search & replace using regexp      |
  | C-h t           | help-with-tutorial | Use the interactive tutorial       |
  | C-h f           | describe-function  | Display help for a function        |
  | C-h v           | describe-variable  | Display help for a variable        |
  | C-h x           | describe-key       | Display what a key sequence does   |
  | C-h a           | apropos            | Search help for string/regexp      |
  | C-h F           | view-emacs-FAQ     | Display the Emacs FAQ              |
  | C-h i           | info               | Read the Emacs documentation       |
  | C-x r m         | bookmark-set       | Set a bookmark. Useful in searches |
  | C-x r b         | bookmark-jump      | Jump to a bookmark.                |


To be continued...
