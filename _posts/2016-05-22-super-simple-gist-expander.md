---
layout: post
title: Super Simple Gist Expander
date: '2016-05-22T12:35:57+09:00'
tags:
- github
- gist
---

I made a small chrome extension to fix one of my annoyances, the text boxes on github gists are way too small.

![BeforeAfter]({{ site.url }}/assets/images/together-1280.png)

Pretty simple codewise. Source code provided on [github](https://github.com/jinpark/gist-expander)

1. Finds out what the window height is and multiplies it by 0.7 (this will be customizable later, but works well for my screen)
2. Resizes the text boxes and gutters to that size
3. Goes onto the page scope and runs `ace.resize()`, which tells the ace editor to resize to fit the container.

Very simple but works great. Anyone who ends up writing long markdown files on github gist, should find it super helpful!

Get the extension [here](https://chrome.google.com/webstore/detail/gist-expander/ekeiajkbcdifndnccdiahmendogegdbp).
