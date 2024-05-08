---
layout: post
title: Writing an Apple TVOS app with (TV)JS and TVML
date: '2016-02-19T06:58:36+09:00'
tags:
- appletv
- apple tv
- tvml
- js
tumblr_url: http://blog.jinpark.net/post/139596438182/writing-an-apple-tvos-app-with-tvjs-and-tvml
---
tl;dr version: I made an Apple TV app with atvjs and it was fun and easy.

I listen to a few podcasts and one of my favorites is Accidental Tech Podcast, a podcast run my Marco Arment, Casey Liss and, my favorite host, John Siracusa. They talk about tech and complain about stuff (mostly Apple) but one of the things they love to hate is the new Apple TV, which is sadly is not available in Korea.

I asked my friend from the US who is visiting to bring one over for me and within a day, I had a working TVOS app running on the emulator. Apple took the javascript on the server idea and allowed developers to create very simple apps using prebuilt templates and js for simple event handling, routing and data manipulation.

Looking at TVJS as a modern javascript developer, it is pretty lacking when compared to current tools and frameworks but someone noticed that and created a wrapper framework called atvjs https://github.com/emadalam/atvjs which simplifies a lot of the repetiveness of the vanilla TVML framework.

I already had a rails server that served videos so it was a breeze connecting an API with atvjs. Creating an app that shows seasons and episodes of a show and plays them back. I used handlebars.js to do some small templating.

You can also inspect your app using safari, similar to a phonegap app, which was a nice surprise. Using that with the log helpers in handlebars helped a lot in figuring out templating problems.

A few small complaints that I had was that it was hard to transfer state when navigating and had to create custom handlers to read from the TVML dom to get state. I’m sure there is a better way to do this but I couldn’t find a way. Also I got stuck when I saw that JSCore in the Apple TV does not log arrays correctly. If you log a standard array with an object in it such as [{cat: 1}] it shows it as {}. It does not affect the logic at all, but it was surprising.

I had a super fun time developing for the Apple TV and I’m already mostly finished with a second app!
