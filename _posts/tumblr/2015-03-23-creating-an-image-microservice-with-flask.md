---
layout: post
title: Creating an image microservice with flask, imagemagick and cloudflare
date: '2015-03-23T09:59:11+09:00'
tags:
- flask
- python
- imagemagick
tumblr_url: http://blog.jinpark.net/post/114405591567/creating-an-image-microservice-with-flask
---
At work (*DramaFever*), we have a microservice that allows for cropping, resizing and caching of images. This allows us to use the same assets that a designer would create and resize it as needed. It also allows for edge caching through a CDN for users to get the images faster. A very useful service.

I saw *firesize* on product hunt recently and I remembered that I wanted to remake our image service on my own, for fun and non-profit. The last project I made was with `ruby` and `sinatra`, so I decided to (very slightly) switch it up and use `python` and `flask`.

I decided on using `imagemagick` for the imaging library because it was easily installed (or preinstalled) on heroku and had a great, simple python api, [wand](http://docs.wand-py.org/en/0.4.2/).

Currently, I just have it resizing based on width and/or height and converting based on filetype. It uses a url scheme of someting like

```
http://images.jinpark.net/image_url?rwidth=optional_width_in_px&rheight=optional_height_in_px&type=optional_file_format_extension
```

To include caching, I used cloudflare’s free tier to allow for edge caching.

Theres some more work to be done, like adding cropping and maybe even seam carving. The biggest change would be to add async processes so requests wont be blocked.

The github repo is [here](https://github.com/jinpark/imageresizer) and you can deploy to heroku with a button!
