---
layout: post
title: Wechat Sticker Maker
date: '2014-10-21T01:32:19+09:00'
tags: []
tumblr_url: http://blog.jinpark.net/post/100565821987/wechat-sticker-maker
---
One of my friends visited me in Korea and she got me hooked into Wechat, another messaging platform. The cool thing is that it allows you to use custom gifs as stickers! (Yes, I know there are other messaging platforms that do this)

I found this tutorial online [https://www.techinasia.com/favorite-animated-gifs-custom-stickers-wechat/](https://www.techinasia.com/favorite-animated-gifs-custom-stickers-wechat/) which pretty much comes down to two steps.

Resize the image to between 150 - 200 px
Optimize the image so it stays under 250 kb
After that, you can save it to wechat and send it to all your friends.

At first I was doing this “manually” using some gif optimizing tools I found online but then I realized that I could do this myself and save myself the hassle of choosing how I want it to be optimized.

I saw that the gif optimizing tool I was using was using [gifsicle](http://www.lcdf.org/gifsicle/) in the backend to do the resizing and optimizing so I used a [node port of gifsicle](https://github.com/imagemin/gifsicle-bin) and set it to resize and optimize the image until it comes under 200kb. Sometimes this is not possible with huge or long gifs so it returns an error when that happens.

This is hosted on heroku and has a very simple (read ugly) web interface that lets you upload a gif or send in a url of a gif and it will resize and optimize it and return it to you so you can save it.

It was a super quick weekend hack that I’m pretty happy with. It does what I want in a quick way. Lots to do if I want to optimize it but I’m ok with it as is for what it does.

http://wechat.jinpark.net (currently down but hacky source code is available [here](https://github.com/jinpark/wechat-gifmaker))
