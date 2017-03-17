---
layout: post
title: Fixing a trivial problem in the most convoluted way possible
date: '2017-03-13T12:35:57+09:00'
tags:
- dns
- raspberry pi
- pi hole
- dietpi
---

![rpi-dns]({{site.baseurl}}/assets/images/rpidns.jpg)

I’m writing a chromecast receiver that works with dash and widevine DRM for work. The chromecast connects wirelessly to my receiver app which is hosted on my work laptop on the same network. When you access the video content on the chromecast, it calls the widevine server to be able to decode the encrypted content, and then decodes the media assets in the browser.

We have a few CORS issues here since the widevine server only has CORS support for a few domains, not including my local domain. The normal way to fix it would be to add CORS support for my local domain in the dev wide vine server, or to temporarily host the receiver app in a domain that has CORS support. 

Instead, I decided to do the most difficult thing and try to edit DNS entries in the router level to redirect back to my laptop. Currently my router is an Airport Extreme which does not have this capability.

I had a few spare raspberry pis left from when I was using them as a media server that I wanted to run OpenWRT on. There were already [prebuilt images](https://wiki.openwrt.org/toh/raspberry_pi_foundation/raspberry_pi) on the OpenWRT website that I tried to use. The problem here was that I either needed to run this between my current Airport Extreme and the modem, or give the raspberry pi wifi. I decided to go the wifi route since I did not want to reimplement the current config of my airport into the new router. 

Long story short, I tried three wifi adapters and they all failed. One failed because the hardware was broken. The second adapter’s drivers did not have the ability to use as an access point. The third just stopped working and I was unable to troubleshoot it. 

Then I decided to try another method. I’ve ran [Pi-hole](https://pi-hole.net/?v=38dd815e66db) before, a DNS server that acts as an adblocker, but it was a pain in the butt compared to just running a chrome extension. This time I didn’t want it for the ad blocking capabilities but for the DNS server that handles the adblocking.

I installed pi-hole through [dietpi](http://dietpi.com/), a mini OS for the raspberry pi running on top of debian jessie. It was easy to setup, but annoyingly not able to be done headless through ssh. Instead, it required a monitor and a keyboard. After I got dietpi and pihole installed, I looked online to see how I could route based on domain. I thought I would have had to create some iptables rules but it was just adding some values to the `/etc/hosts` file and restarting the `dnsmasq` service.

After I set that, I set the default dns server on my router to point to my pi hole server and then everything was set. I was able to point any domain wherever I wanted and as long as you were connected to the airport extreme, you were redirected correctly.

Next time I would need to do something like this, I would just run a dns server locally instead of on a raspberry pi. You can `brew install dnsmasq` easily and handle your dns rules locally. 

NOTE: I realized after I did all this that the chromecast has its dns hardcoded internally to google's DNS. So everythign I did does not work.... I ended up buying a new router
