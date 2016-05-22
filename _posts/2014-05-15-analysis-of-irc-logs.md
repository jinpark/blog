---
layout: post
title: Analysis of irc logs
date: '2014-05-15T21:38:05+09:00'
tags: []
tumblr_url: http://blog.jinpark.net/post/85872952662/analysis-of-irc-logs
---
I’ve been on IRC for a while (5 years or so).

I made a lot of friends and talked to a lot of different people and watched myself and others change over time.

Recently, vertigo (one of the early members of the IRC chan I was/am in) got me ~7 years of logs, which came out to be ~2 million lines.

I loaded it into mongodb (so I can get more used to nosql), installed pymongo and decided to do some sentiment analysis on it. I used the great TextBlob module to quickly do the sentiment analysis.

There were a few things that vertigo and I wanted to find out.

One was who is the most positive and negative in the channel. I did some VERY basic analysis and looked at the average sentiment polarity and got some interesting and some obvious results.


![sentiment by user]({{site.baseurl}}/assets/images/sentiment-users.png)

complex (used to be) our resident troll-ish person. Worked perfectly that he was the most negative. Another user PF used both lowercase and uppercase versions of his nick and we can see that both of them are almost the same.

Another question was since vertigo gets some “help” from certain substances during the weekend, is he more positive during the weekend compared the weekdays.

![sentiment by day]({{site.baseurl}}/assets/images/sentiment-day.png)

As we can see, there is a slight trend but it does not seem to be significant. Also vertigo likes tuesdays for some reason.

Next step is to look at some time series and see how people changed over time!
