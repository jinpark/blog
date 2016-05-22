---
layout: post
title: Creating an Adaptive Streaming Video Pipeline for Web
date: '2016-04-27T11:08:55.847Z'
tags:
- video
- dash
---
As I have previously written before, I have a small video streaming website (and app) for watching simpsons. Currently, it streams 1080p h264 mp4s with ~320 aac audio. While this is fine for local use and users with fast internet, it does take a while to start and seek since the amount of data it needs to buffer is pretty large.

The way that people have gotten around this and other problems is with adaptive bitrate streaming. THe current standard is using HLS and DASH. HLS is currently the most popular adaptive streaming method created by Apple for their iOS devices and has pretty good support across multiple devices. DASH is the new standard created by Akamai, Microsoft, and other large companies under the MPEG group. DASH is a universal standard that tries to be better than the vendor specific implementations such as HLS.

The current encoding workflow is to first take the source file, run it through ffmpeg to make 3 renditions, 560Kbs at 512px, 1750Kbs at 720px, 3000Kbs at 1280px with aac passthrough audio, since the file size for audio differences are negligible. One note here is that you need to segment the mp4 here with keyframes. The keyframes will set what the fragment size will be so you will need to set it to what works for you. My current setup is the standard recommended 2 second fragments.

Here is an example of converting the video file with `ffmpeg`, fragmenting the file with `mp4fragment` from bento4, and then creating the manifest with `mp4dash` from bento4.


```
ffmpeg -i s01e02-small.mp4 -c:v libx264 -c:a aac -strict experimental \
-b:v 1M -b:a 128k -movflags frag_keyframe+empty_moov \
-vf scale=1280:-2 -b:v 3000k -x264opts 'keyint=48:min-keyint=48:no-scenecut' \
s01e02-small-1280.mp4
```

```
mp4fragment s01e02-small-1280.mp4 s01e02-small-1280-fragment.mp4
```

```
mp4dash --media-prefix=s01e02 --mpd-name=s01e02.mpd --output=s01e02 s01e02-small-1280-fragment.mp4 s01e02-small-720-fragment.mp4 s01e02-small-512-fragment.mp4
```

The next step is to actually split the mp4 files. I'm using bento4 to fragment the mp4 files and create the manifest. I run the mp4fragment command with the three video renditions and it creates split f4m files and a mpd manifest. 

The f4m files and manifest are served by nginx and the routes to the manifest are stored in the rails backend where its served to videojs in the frontend. 

The next step is to automate all this and this can be easily done by making a rake task within the rails backend and passing in the location of the source file and some basic info about the episode. It will create the manifest and segmented files and also create the episode object as well.
