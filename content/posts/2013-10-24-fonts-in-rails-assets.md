---
author: rpbaltazar
categories:
- Computer Science
date: "2013-10-24T08:25:49Z"
tags:
- assets
- custom fonts
- rails 4
- ror
title: Fonts in rails assets
---
In order to use a custom font in a Rails 4 project, you can either put it under public folder (and configure the css path accordingly) or you can load it from assets folder.

First of all, I personally recommend that you read the [assets pipeline entry](https://edgeguides.rubyonrails.org/asset_pipeline.html). This will give you a fairly good idea on how to do it.

Nevertheless, given the two options here it goes:

**Option 1 &#8211; **load the font file from the public folder****

  1. Copy the font file to public/fonts/<whatever path you want>
  2. configure your css file to load the needed path
      1. Add the following to your css file
        ```css
          @font-face {
            font-family: 'VanCondensed';
            src:url("/fonts/VanCondensed-Regular.otf");
            font-weight: normal;
            font-style: normal;
          }
        ```

**Option 2 &#8211; **load the font from the assets folder****

  1. Copy the font file to app/assets/fonts/<whatever path you want>
  2. Update your config file, so the project knows that it has to load the fonts folder
      1. `config.assets.paths << Rails.root.join('app', 'assets', 'fonts')`
  3. configure your css file to load the needed path
      1. Change the css file extension to css.erb
      2. Add the following to your css file
        ```css
          @font-face {
            font-family: 'VanCondensed';
            src:url("<%= asset_path('VanCondensed-Regular.otf') %>");
            font-weight: normal;
            font-style: normal;
          }
        ```
  4. Restart your server

&nbsp;
