---
layout: post
title: Sending text message on a schedule with twilio and at
date: '2013-12-22T01:24:00+09:00'
tags:
- twilio
- sms
tumblr_url: http://blog.jinpark.net/post/70762225754/sending-text-message-on-a-schedule-with-twilio-and
---
My friend Anna is in Canada right now. Canada has delicious things that America does not have and I would like Anna to bring me some.

I gave her a small list of things but she said she would forget and would prefer for me to text her what I wanted Thursday morning (which is when she would have time to buy stuff). That is a few days away and I was sure I would not remember when Thursday rolled along. So I decided to set up a script somehow to send a text message to Anna on Thursday morning. I had a server running, a twilio account and I knew linux would have some sort of command to set up something time based (most likely cron).

I had a phone number on Twilio before when I used to host a text message service for App Academy friends on who they would be paired with the next day. (I will probably write a small blog post on that later)

Setting up the ruby script was very simple. I just used the ruby example on Twilio docs and changed some of the config values. I tested it by sending a message to myself and it worked perfectly.

I knew I wanted to set something up to shoot off this script at a specific time. I knew that cron would work but when I googled, it seemed that the “at” command was a much better choice. Cron was made for repeated schedules while “at” was for one-offs. Running it was extremely simple. To send something off at a specific time, it was just

at 7:00 am


Or even

at now + 2 min


Awesome simple syntax.  There are more examples here. To check out all scheduled “at” jobs. It was just

at -l


So I just set up

ruby <location of file> | at 9:00 am Dec 26 #which is thursday


and checked it with

at -l


and it was done. Woot!
