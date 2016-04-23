---
layout: post
title: '"Crunch time" - Writing code for a deadline that has already past!'
date: '2015-07-13T05:25:05+09:00'
tags: []
tumblr_url: http://blog.jinpark.net/post/123967996877/crunch-time-writing-code-for-a-deadline-that
---
So continuing from my previous post where I wrote a podcast site using jekyll and markdown and then rewrote the whole site in django…

When creating a podcast site, one of the most important parts is to actually play audio. I looked at a bunch of different radio and podcast sites (http://monocle.com/radio/ and http://serialpodcast.org/ jumped out at me for being better than most) to get some inspiration and found that the majority of them are either using their own custom html5 audio player or using soundcloud. As I’ve had “problems”* using soundcloud before, I decided to go the html5 audio way.

I went on a google binge trying to find a library that would let me control the styling and experience of html5 audio without me having to do too much work and I came upon amplitude.js. It had great documentation, was fairly easy to use and the authors were very responsive. I asked about a problem on their gitter chat and got a response and fix within minutes! The only custom work I did was to create a range element that was clickable and linked with seeking audio. I have it here if you want to take a look. It was mostly based on a css tricks link page with some css hacks to get the colors to work.

All was well except that once in a while I was unable to play audio until I refreshed and it kept getting worse and worse until nothing played. I notified the library authors about this but they couldn’t find a reason why it was failing.

A few days ago, Bobby, Ahnmin and Jackie finished editing the new episode of Something Sunshine and wanted to post it up. They were able to upload and publish an eisode by themselves and everything (almost) worked! The only problem was that none of the episodes played……

Crunch time…

Just to get something working, I hacked it so each button linked to a html5 audio element and just played/paused, without allowing for seeking. This was fine for a temp job but I knew we wanted full functionality before we started promoting.

I spent a day writing a quick jquery library that would give me the same functionality as amplitude.js but actually work. I came up with jquery.audio.js, which is also a quick hack of a jquery method. I’m kinda proud of it (even though the code is horrible) because of how fast I was able to get it out.

Check it out and please send pull requests to clean up the code!

Look at my previous post to figure out what those “problems” were.
