---
layout: post
title: Writing Desktop Apps with Electron
date: '2015-10-17T12:29:59+09:00'
tags: []
tumblr_url: http://blog.jinpark.net/post/131356288527/writing-desktop-apps-with-electron
---
One of my long term ‘projects’ was to figure out a way for me to look at my todo list more frequently. I spend most of my time on the computer at a browser window, at the terminal or at the IDE, so I needed something that would stay on top of all of those and force me to look at it. The hack I originally had was to make a todo app (Any.do) window transparent and force it above all the other windows. Afloat was what I used, and it required a decent amount of weird hackery and didn’t even behave consistently across restarts. While this kinda worked, all the apps enforced minimum window sizes and generally did not fit my needs. Time to keep looking…

Continuing from my last post about ionic, Electron, can be seen as a phonegap for desktop apps. It embeds a nodejs runtime which has connections to native APIs into a desktop app so you can use web technologies to build up your desktop app. Unlike ionic, it does not force you to use a specific framework or give you any native looking styling. It runs a renderer process, which runs the web frontend chromium and a main process, which is the node backend that has access to the native APIs. They talk to each other using IPC and/or RPC. I found menubar on github which allowed you to run mini apps on the menubar and I had an idea. I really like google keep on mobile, I wonder what I can do with it as a native app.

I tried the menubar example app and then quickly modified it to point to keep.google.com and it just worked. I was more or less pretty happy with how it looked and its performance! I created a new icon, made it preload the window so it works a bit faster, added a clean way to quit the app (right click on the icon) and then made it transparent by using some css hackery and stay on top so I can be reminded all the time of what I need to do for the day.

The next test app I made was a pairing timer. I’m starting to teach programming more and I want to bring the joys of pairing to a new group of people. What I wanted here was a pairing app that has a set time (15 minutes), shows a notification and makes a sound when the times up. I ended up using the html5 notifications for mac and tray bubbles for windows and sounds using html5 audio. Most of these I was very familiar with due to it being exactly the same as front end development. Overall, it took a little bit over an hour to code up and have it up and running locally. You can download the mac version here. The source code is here. Feel free to make issues for bugs or feature requests.

The problems I had were mostly at the end. Packaging the app became a pain in the butt, partly because I misunderstood what the packager was doing and the fact that building for windows required wine. Another problem was that for windows, you either need to run the exe file in the same folder as the node runtime or package it into an installer. The problem with the installer is that it requires it to be codesigned, which costs at least 200 usd for a certificate. For now, I’ll just create a shortcut and run it that way but we’ll see how that goes.

Overall, I had a great experience with electron so far and a great first foray into desktop app development!
