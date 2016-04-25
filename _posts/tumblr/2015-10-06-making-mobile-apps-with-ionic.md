---
layout: post
title: Making mobile apps with Ionic
date: '2015-10-06T22:20:04+09:00'
tags: []
tumblr_url: http://blog.jinpark.net/post/130656646607/making-mobile-apps-with-ionic
---
As a developer that mostly works on the web, mobile apps always seemed like it was a big pain to learn. I don’t have java or obj-c/swift experience and while I did take an android MOOC course sponsored by google, I came out with more of a basic understanding rather than a practical understanding.

Before that, I fooled around with phonegap, which is a wrapper around webviews of different mobile OS-es. It provides a few plugins to allow interaction with the native APIs, such as the camera, but at the time, I did not feel that it was easy to use.

After that I found ionic. This was pre 1.0 when I did not have much if any angular experience. I explored through the documentation and thought it was great if I could ever figure out how angular works :D

A few years after that, a friend and I decided to start a business focusing on a mobile app. I chose Ionic as the platform I wanted to use and started hacking on it. There were a lot of small inconsistencies with it but it was not too difficult to go around it. I’m still working on this app.


Then I built an app for my friends podcast, Something Sunshine. It was a very simple app, a list view leading to a detail card view. The only problem was getting streaming to work. None of the standard solutions for playing file media worked out of the box and the rest of the streaming solutions were hacky and inconsistent. I ended up using straight html5 audio with an angular wrapper but it is still an incomplete product since it has problems streaming when the screen is off. You can still find the app on ios and android


I then took what I learned from that app and created another app for my friend’s wedding. This one is more fully featured, using a side menu with many different views, using the google maps api with directions and accessing the native camera API for taking selfies. I also ended up using the instagram api and used parse as a backend and a poor but manageable admin page. It is also out on ios and android

Overall, I’m pretty happy with Ionic as a mobile development platform. I’ve hit its limitations a few times but the development team is super quick at answering questions and they have a great development platform with a nice CLI and development app viewers. The only problem I saw was a lack of fully open source large scale apps from which to view. There are many small snippets but nothing that resembles something along the lines of facebook in scope.
