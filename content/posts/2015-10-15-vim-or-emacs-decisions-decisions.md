---
author: rpbaltazar
categories:
- OSx
date: "2015-10-15T10:19:20Z"
guid: http://balazar.net/random/?p=132
id: 132
image: /wp-content/uploads/2015/10/cartoon284.png
tags:
- emacs
- mac
- text editor
- vim
title: Vim or Emacs&#8230;. decisions decisions&#8230;.
url: /2015/10/15/vim-or-emacs-decisions-decisions/
---
This will be a part of a series where I&#8217;ll be trying the devil&#8217;s question. Vim, or Emacs.
I do understand that for taking a real big advantage from any of both, you should be a long-term user, as it implies a lot of configuration and it takes a lot of personal taste.

Nevertheless, let the journey begin&#8230;

I&#8217;m currently using a Macbook Air with Yosemite in it.

Emacs&#8230; let&#8217;s do it.
<!--more-->

  * Installation
    `<br />
brew install emacs --HEAD --use-git-head --with-cocoa --srgb<br />
` </p>
    If you didn&#8217;t link emacs app to your applications folder, I&#8217;d suggest you to do so.

    `<br />
brew linkapps emacs<br />
` </li>

      * Once you start emacs, you can close it by pressing:
        `<br />
C-x C-c<br />
`
        Please note that C means Control
      * Keyboard basics
        <div class="table-responsive">
          <table id="keyboard-basics" style="width:100%; "  class="easy-table easy-table-default tablesorter  " border="0">
            <tr>
              <th class=' ' >
                Key combination
              </th>

              <th class=' ' >
                Action
              </th>
            </tr>

            <tr>
              <td >
                C-p
              </td>

              <td >
                Up one line
              </td>
            </tr>

            <tr>
              <td >
                C-n
              </td>

              <td >
                Down one line
              </td>
            </tr>

            <tr>
              <td >
                C-f
              </td>

              <td >
                Forward one character
              </td>
            </tr>

            <tr>
              <td >
                C-b
              </td>

              <td >
                Backward one character
              </td>
            </tr>

            <tr>
              <td >
                C-a
              </td>

              <td >
                Beginning of line
              </td>
            </tr>

            <tr>
              <td >
                C-e
              </td>

              <td >
                End of line
              </td>
            </tr>

            <tr>
              <td >
                C-v
              </td>

              <td >
                Down one page
              </td>
            </tr>

            <tr>
              <td >
                M-v
              </td>

              <td >
                Up one page
              </td>
            </tr>

            <tr>
              <td >
                M-f
              </td>

              <td >
                Forward one word
              </td>
            </tr>

            <tr>
              <td >
                M-b
              </td>

              <td >
                Backward one word
              </td>
            </tr>

            <tr>
              <td >
                M-<
              </td>

              <td >
                Beginning of buffer
              </td>
            </tr>

            <tr>
              <td >
                M->
              </td>

              <td >
                End of buffer
              </td>
            </tr>

            <tr>
              <td >
                C-g
              </td>

              <td >
                Quit current operation
              </td>
            </tr>
          </table>
        </div>

      * Basic functions and their shortcuts
        <div class="table-responsive">
          <table id="functions-basics" style="width:100%; "  class="easy-table easy-table-default tablesorter  " border="0">
            <tr>
              <th class=' ' >
                Key combination
              </th>

              <th class=' ' >
                Function
              </th>

              <th class=' ' >
                Description
              </th>
            </tr>

            <tr>
              <td >
                C-x C-s
              </td>

              <td >
                save-buffer
              </td>

              <td >
                Save the current buffer to disk
              </td>
            </tr>

            <tr>
              <td >
                C-x u
              </td>

              <td >
                undo
              </td>

              <td >
                Undo the last operation
              </td>
            </tr>

            <tr>
              <td >
                C-x C-f
              </td>

              <td >
                find-file
              </td>

              <td >
                Open a file from disk
              </td>
            </tr>

            <tr>
              <td >
                C-s
              </td>

              <td >
                isearch-forward
              </td>

              <td >
                Search forward for a string
              </td>
            </tr>

            <tr>
              <td >
                C-r
              </td>

              <td >
                isearch-backward
              </td>

              <td >
                Search backward for a string
              </td>
            </tr>

            <tr>
              <td >
              </td>

              <td >
                replace-string
              </td>

              <td >
                Search & replace for a string
              </td>
            </tr>

            <tr>
              <td >
              </td>

              <td >
                replace-regexp
              </td>

              <td >
                Search & replace using regexp
              </td>
            </tr>

            <tr>
              <td >
                C-h t
              </td>

              <td >
                help-with-tutorial
              </td>

              <td >
                Use the interactive tutorial
              </td>
            </tr>

            <tr>
              <td >
                C-h f
              </td>

              <td >
                describe-function
              </td>

              <td >
                Display help for a function
              </td>
            </tr>

            <tr>
              <td >
                C-h v
              </td>

              <td >
                describe-variable
              </td>

              <td >
                Display help for a variable
              </td>
            </tr>

            <tr>
              <td >
                C-h x
              </td>

              <td >
                describe-key
              </td>

              <td >
                Display what a key sequence does
              </td>
            </tr>

            <tr>
              <td >
                C-h a
              </td>

              <td >
                apropos
              </td>

              <td >
                Search help for string/regexp
              </td>
            </tr>

            <tr>
              <td >
                C-h F
              </td>

              <td >
                view-emacs-FAQ
              </td>

              <td >
                Display the Emacs FAQ
              </td>
            </tr>

            <tr>
              <td >
                C-h i
              </td>

              <td >
                info
              </td>

              <td >
                Read the Emacs documentation
              </td>
            </tr>

            <tr>
              <td >
                C-x r m
              </td>

              <td >
                bookmark-set
              </td>

              <td >
                Set a bookmark. Useful in searches
              </td>
            </tr>

            <tr>
              <td >
                C-x r b
              </td>

              <td >
                bookmark-jump
              </td>

              <td >
                Jump to a bookmark.
              </td>
            </tr>
          </table>
        </div></ul>

    To be continued&#8230;..
