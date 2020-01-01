---
layout: post
title: My Download and Streaming Setup
date: '2019-12-28T01:50:29+09:00'
tags:
  - plex
  - streaming
---
I went from 2 posts a year to 1...

This is going to be a quick overview for setting up a home streaming service that (mostly) automatically downloads new episodes.

You'll need 
1. Home server with lots of storage
2. Static IP or a dynamic DNS 
3. Fast-ish upload speeds (Above 20-30 mbits for full streaming)

Software that I use
1. [Plex](https://plex.tv) (requires subscription for all features and paid client apps)
2. [Sonarr](https://sonarr.tv/)
3. [Transmission](https://transmissionbt.com/)
4. [Filebot](https://www.filebot.net/) (paid software)

Plex is home streaming software that allows you to basically create your own streaming service. If you have your files in a specific structure that Plex can read, it will create a browsable directory of your shows that you can access through their (web, mobile, etc) clients. There are also apps for smart TVs. The server component allows you to set up different quality streams as well as download them later. You usually just need to download the Plex Media Server for your OS and let it run as a daemon or service.

Sonarr checks for and downloads new episodes of your shows, also known as a PVR (Personal Video Recorder). You set it up by feeding it RSS feeds of where it can download shows (either by torrents or usenet) and using a torrent client, Transmission in this case, and it downloads new shows when it gets released. It also renames and moves files to work with Plex.

Transmission is a torrent client which works with Sonarr. It also can be controlled remotely through a web server interface.

Filebot is for shows or movies that I am not able to get through Sonarr, or if I batch download shows. It can check different metadata sources such as The Movie Database to correctly rename files for Plex. 

The overview is to setup Sonarr with rss feeds to shows, which will trigger Transmission to download them. Sonarr will take those completed downloads and rename them to fit Plex's requirements and then also move them to the Plex directory. Plex will then index the files and allow it to be streamed.

A few things that you should keep in mind.
1. Pay for Plex to allow for "syncing". Syncing in Plex allows you to download shows to your client device instead of streaming. 
2. Setup Transmission so it has authentication. It's a safeguard to make sure that no one else can access your Transmission instance.
3. Sonarr is sometimes late on getting data for new shows. You might need to wait a week or two before it starts knowing when to download or what metadata it should look for.
4. You might need access to your server outside your network for maintenance. I suggest a VNC or RDP type solution. I'm using [Guacamole](https://guacamole.apache.org/) since its very easy to connect through any web browser.

I'm currently running this on Windows 10 right now, mostly due to the fact that I need Windows for a few govt and bank things. It doesn't use a lot of cpu (when its not transcoding) and its low maintenance.