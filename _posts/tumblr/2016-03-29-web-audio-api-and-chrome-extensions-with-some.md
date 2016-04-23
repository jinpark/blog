---
layout: post
title: Web Audio API and Chrome Extensions (with some hacky js hackery on the side)
date: '2016-03-29T06:08:46+09:00'
tags:
- chrome extensions
- web audio api
- hacks
tumblr_url: http://blog.jinpark.net/post/141891260657/web-audio-api-and-chrome-extensions-with-some
---
I was talking to another developer asking me what she needed to do to do some cool audio visualizations with soundcloud.

The first thing I thought of was use the soundcloud API, download the file, run it through an audio analyizer and then do some visuzliations with d3 or some other visualization framework.

She told me that she wanted to do it in real time and as a chrome extension. Hmmmm. I have done some chrome extension stuff before but nothing with audio analysis and visualization.

I looked up web audio visualizations on google and found this from mdn (https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API/Visualizations_with_Web_Audio_API) and this http://webaudioapi.com/samples/visualizer/ . The basic idea behind those were to create an audio element, feed it into the audio context from the web audio api and use the web audio analyzer to get frequency data out of it to visualize.

I spent a few hours splunking through the soundcloud js code to figure out where and when they were initializing the audio object and try to hook into it. Using the chrome debugger, I was able to figure it out, but due to (valid) limitations on the chrome extension api, I was not able to connect the js variable of the audio element to the js in the chrome extension.

I looekd online again and found a hacky hack where you monkey patch the createElement method and keep track of all the audio elements created by createElement and then you can access the audio element through the dom. This method required another hack, since chrome extensions don’t allow you to run js in the page scope. I created a script element, made a string of js of the createElement hack and then appended it to the script tag. I appended the script tag to the top of the page and then I was on my way.

I cleaned up the code and had a working example, using content scripts to handle the audio and web audio api part and then passing the formatted frequency data to the popup js code where the visualization happens.

This worked for soundcloud, but how about other sites?

Since I had a better idea of what I was looking for at this time, I searched for audio eq chrome extensions (since an EQ would require the same access to the audio as a visualizer) and to my surprise, I found a few. I found one that was on github https://github.com/ejci/Chrome-Audio-EQ and took a look at the code. While it says it only works for only audio and video elements, there was some in progress code https://github.com/ejci/Chrome-Audio-EQ/blob/master/extension/background/background_v2.js which uses something called tabCapture from the chrome api.

From what I found, this is commonly used for webRTC to share your screen for screensharing, but this can also be used to capture all audio coming out of your current tab, which is exactly what I needed.

Since using this api required my code to not be in the content scope but in the background scope. I made modifications to my messaging code but kept most of the business logic the same. I needed to manually close the audio context and the tabCapture stream to be able to the switch between tabs and allow the audio stream to be passed back to original tab.

The code is here https://github.com/jinpark/audio-visualizer and the original super hacky code is in this commit https://github.com/jinpark/audio-visualizer/tree/3401a5ffae729c59b99600f5b9288980f9e3c7fe

Thanks to Soeun for the idea! http://mojosoeun.github.io/
