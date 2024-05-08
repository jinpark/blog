---
layout: post
title: Quick Particle Project to Display Air Quality at a Glance
date: '2017-05-30T12:35:57+09:00'
tags:
- particle
- air quality
- particle photon
- webhooks
---

I’ve been waiting for World Air Quality Project to release their JSON API for normal users for a few years now. They finally did and now I can finish my first particle project.

I’m going to be using a [Particle Photon](https://www.particle.io/products/hardware/photon-wifi-dev-kit) , [an Internet Button](https://www.particle.io/products/hardware/internet-button) , [the World Air Quality Project JSON API](http://aqicn.org/json-api/demo/) and [Particle Webhooks](https://docs.particle.io/guide/tools-and-features/webhooks/) .

First, I got an API key from aqicn.org by entering my info [here](http://aqicn.org/data-platform/token/#/). I then found my nearest monitoring station number by finding my current latitude and longitude and searching for my nearest station using [this api](http://aqicn.org/json-api/doc/#api-Geolocalized_Feed-GetGeolocFeed) and using that station id to get the AQI info from that station using [this api](http://aqicn.org/json-api/doc/#api-City_Feed-GetCityFeed).

Now I can call the API and get my current AQI (Air Quality Index). The next step was to set this up to be consumed by the Photon. This can be done by setting up a webhook within the Particle Console. Set up a new webhook to GET the air quality endpoint, and use the response template to just return the AQI value. The response template uses the mustache templating engine, so you might need to fiddle around with it.

Time to write the firmware for the Photon! I’ll just go over the main points.

First, include the InternetButton library and instantiate it. In the setup block, subscribe to the webhook so it receives the AQI values and create a handler function that converts the AQI value to a RGB value set that can be easily ingested by the internet button. Call the webhook every 60 minutes, and turn on all the LEDs to those values a few seconds after you make the call. That should give the API enough time to respond.

The full code is below.

{% gist 83f30d36fce5c1d0da4ae90f33ea269a %}

This was a fun quick 1 hour project that should hopefully let me know when I should put my mask on!

