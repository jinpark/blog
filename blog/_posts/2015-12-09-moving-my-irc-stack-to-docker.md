---
layout: post
title: Moving my IRC stack to Docker
date: '2015-12-09T02:05:39+09:00'
tags:
- docker
- irc
tumblr_url: http://blog.jinpark.net/post/134843721847/moving-my-irc-stack-to-docker
---
Recently, I got a good deal from a cloud provider company called cloudatcost (not linking on purpose here since they seem pretty sketchy) and wanted to move some of my personal services on there.

My current IRC “stack” (inspircd for the irc server, znc as an irc bouncer and common, an irc bot) has been working more or less pretty great with no problems on Digital Ocean for five years or so. But since I’m cheap, wanted a project to do, and I like making my life more difficult, I decided to move it to a cheaper, less reliable and slower host.

The first service I moved over was znc, an IRC bouncer. Since I wanted to do this the easiest way possible, I looked online and found https://github.com/jimeh/docker-znc , a premade dockerfile to run znc. I took my older znc config, made a few slight changes and it was ready to go.

The cool thing about this dockerfile was that it had a way to build znc packages on startup. It just ran znc-buildmod on any *.cpp file it found in a specific folder. Normally, that would have been fine but the module I wanted to use (a module that gave push notifications on palaver) did not work that way, and this specific module required you to run a makefile to get it built. I just ended up exec-ing into the container and running make, and since the module folder is mounted, it would persist the module through restarts.

The second service I moved over was my irc bot, named common, (blessed be based bob). It first ran as a phenny (v2) bot. Then the bot was upgraded to jenni by the developers and then to willie and now sopel http://sopel.chat/.

This was fairly simple to port to docker as well. Made a dockerfile where it installed sopel through pip, created a new sopel user and ran sopel through that. Like znc, it required you to run as a non-root user. I also did a volume mount to share the .cfg files and the modules. The only problem was porting my old, poorly written and documented custom modules to the new version of the bot. Dockerfile at https://github.com/jinpark/sopel-docker

Last but not least was inspircd, the irc server. I saved this one for last because I thought this would be the most complicated. Turned out it was one of the most simple. The only difference here was that I had to pre-compile the inspircd binary beforehand within the docker container. I just did that by docker runing into a bash shell and running configure and make on there while outputting the built output into an attached volume. After that I could just move my config files, run ./inspircd start and we would be good to go.

Overall, moving all my irc services to docker gave me a chance to update my old crufty services while also providing a portable way to change vps providers when the time comes. It was also a lot easier than I expected, most of the troubles were based on the specific software I was using more than the docker stuff. The small docker troubles I ran into (cached images caused apt-get to fail) were things I ran into before when fooling around with docker.

Goooo docker!

UPDATE: The next day after I wrote this post, my vps got completely hosed. Unresponsive customer support and the vps is completely disconnected. Good thing I made my services into docker containers so its super easy to move.
