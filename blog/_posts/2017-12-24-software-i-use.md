---
layout: post
title: Software I Use Daily
date: '2017-12-24T01:50:29+09:00'
tags:
- mac
- server
- software
---
I've been changing my computers pretty frequently recently due to hard drive failures, un-hackintoshing my computer, laptop screen failures etc, so I had to reinstall and re-setup my computer a bunch of times. 

I had a chance to review my setup and see where I could make upgrades and which stuff I can keep. Kind of a spring cleaning for my computer.

### Essentials

1. [Transmit for Mac](https://panic.com/transmit/)
    - My favorite software to move files around to and from servers. It has access for `s3`, `backblaze b2`, `ssh`, `ftp` and whatever else you can think of. 

2. [Dropbox](https://www.dropbox.com/)
    - Holds my 1Password data, and has over 10 years of files. I'm actively looking for a replacement that I can use as a drop in replacement but I haven't found it yet.

3. [1Password](https://1password.com/)
    - Saves all my passwords. Makes it pretty fast for me to create and retrieve complex passwords.

4. [Chrome](https://www.google.com/chrome/browser/desktop/index.html)
    - Its fast and its dev tools are the best. I have `ublock origin`, `the great suspender`, `google dictionary`, and `disable html5 autoplay` plugins installed. 

5. [Opera](http://www.opera.com/)
    - Thinking about changing to Opera full time but doesn't have all the extensions as chrome yet. Runs on the same engine so its pretty fast and comes with free browser based vpn. By far the easiest VPN I use that doesn't seem to steal my data (hopefully)

6. [Visual Studio Code](https://code.visualstudio.com/)
    - I've been a staunch user of Sublime Text for a long time but I took the chance to dip my toes into atom and VSCode. Both were fine but VSCode seemed to work better for me. The great markdown integration, built in linting, and a bunch of features that doesn't seem to slow down the program.

### Terminal Stuff

1. [iTerm2](https://www.iterm2.com/)
    - Normal terminal is fine but doesn't have `tmux` integration, which is essential for me for when I `ssh` into servers.

2. [tmux](https://tmux.github.io/)
    - terminal multiplier, like a newer `screen` or older version of tabs. I kinda hate the `ctrl-b` key binding but I use `ctrl-a` for go to the beginning of the line that I can't seem to change it.

3. [fish shell](https://fishshell.com/) 
    - Fish shell just seems like a modern shell. The configuration is done through a slick locally hosted website, the API makes sense and is pretty fun to use. The one problem is that the syntax is pretty different from bash which makes using some CLI programs that are based on bash harder to use.

4. [solarized dark themes](http://ethanschoonover.com/solarized)
    - I like solarized dark.

### Home Server

1. [Plex](https://plex.tv/web)
    - Serves up my video files that I somehow have. Mostly stuff that isn't easily obtainable through legal sources. It's just a super nice piece of software. (I have a Plex Lifetime subscription. I just want to give them money!)

2. [Sonarr](https://sonarr.tv/)
    - Schedules regular downloads of shows I can't get here due to licensing issues. Coupled with Plex, this makes a killer home media service.

3. [Guacamole](https://guacamole.apache.org/) 
    - Allows for rdp/vnc/whatever to be accessed through the web. I've been `noVNC` for a little bit but guacamole comes with auth and multiple users and works well in windows (at least with docker).

4. [Caddy](https://caddyserver.com/)
    - A simple http web server. Super easy setup and https right out of the box. Just a great front end to all the web services I run on the server.

5. [The Lounge](https://thelounge.github.io/)
    - A web based bouncer and client for IRC. A fairly new thing for me, but it totally replaced textual, my previous irc client. Since its just a web app, you can run it on your phone and also, since its a PWA, web push and notifications work on any browser that supports it. So even on my android phone, it works like a true native app.


### Services (that I pay for)

1. [Paperspace](https://www.paperspace.com/)
    - A workspace as a service that allows me to have a windows workstation whenever I need it. Pricing is super cheap, works amazingly well for being across the globe, and pretty fast customer service. 

2. [Newsblur](http://www.newsblur.com/)
    - My `RSS` reader of choice. Lays out the feed really cleanly, downloads the content beforehand so its really quick to retrieve content and has its own readability-like thing.

3. [Naver Music](http://music.naver.com/)
    - I got this for "free" after buying their Wave voice assistant speaker. Well laid out interface for their android app, gets music up really quickly. Good replacement for Spotify. Small note, their web interface sucks.

