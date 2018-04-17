---
layout: post
title: IRC Bot to Alexa Skill
date: '2018-04-17T01:50:29+09:00'
tags:
- IRC
- Willie
- Bot
- Alexa
- Echo
- Flask
- Flask-Ask
---
I've been running an IRC bot on a small network that I run for a while (10 years?). One of its features is that it can tell you about the air quality in the general vicinity of where you are (assuming you have added your location data previously). It's a fairly simple little python script that just calls a geocoding API to convert a location to a latitude and longitude and uses an air quality API to return the AQI (Air Quality Index) value. The code for that is available [here](https://github.com/jinpark/phenny-modules/blob/master/air-quality.py). I talked about a IOT version of this in a [previous post](https://www.jinpark.net/blog/2017/05/Quick-Particle-Project-to-Display-Air-Quality-at-a-Glance).

I've been fooling around with different (4!) voice assistants at home and realized that for Alexa, there was no skills to check air quality outside of the US for US based Alexa devices, which mine was. I wrote a small Alexa skill a while back for playing back Simpsons so I knew that I could bang out a quick air quality skill without a problem.

I used [Flask-Ask](https://github.com/johnwheeler/flask-ask) as the backend framework to handle the boilerplate to interface with the Alexa SDK. The only thing I added was to find a list of 5000 largest cities in the world and add those as a custom slot. Currently, the Alexa SDK only provides US, GB and a few other countries for city slots. I just created a long text file with the list of cities and added that into the Alexa skill console.

One other thing that you need to do is to create and add a privacy policy to the app. I took a standard privacy policy since I was not recording any personal data from the user and just modified it a bit to fit this app.

This whole project took about an hour or so between the time I woke up and had breakfast, so there are more than a few things missing. I'm currently working on accessing the location provided by Amazon for each user instead of requiring the user to say the location when activating the skill. Also, I need to cache the geocode results so I don't hit the geocode api repeatedly. 

The code is available at https://github.com/jinpark/airquality-alexa . 

