---
layout: post
title: Converting a CLI to a web service
date: '2023-01-10T01:50:29+09:00'
tags:
  - kcc
  - web
  - programming
  - python
---

Surprisingly, I've been getting "a lot" (50 hits) of traffic on my [using kcc on m1 blog post](https://www.jinpark.net/blog/2021/05/Using-KCC-With-a-M1-Mac). I even had a few people email me for help on how to get it working.

I realized that the whole process is a bit convoluted to set up if you are not used to the command line so I thought of making a web service for this.

The basic idea here is that kcc already has a cli that you can use to convert files into specific ebook formats. This just needs to be wrapped up in a nice web service and that should be done! Easy peasy!

Theres a few snags here to get this to work correctly.

1. To convert a file, KCC takes a long time to convert a comic, especially if the comic is large with many pages.
2. Converting a comic takes a lot of CPU resources. Running many of these conversions in parallel will make any server unhappy.
3. Comics that people upload and the resulting converted files are fairly big. To store these will end up being expensive in the long run.

Theres many ways to solve these issues but I took the easy way and decided that
1. I want to keep this running on a simple VPS
2. Don't want to spend too much money keeping this up

I ended up creating a queue based web service.

The service is made up of 3 main parts.
1. Backend/Frontend run by [FastAPI](https://fastapi.tiangolo.com/) and Jinja for templating and some simple JS for basic form handling. There was no reason to use anything fancy here so I stuck with a straightforward old school backend that renders html. The data storage is by redis.
2. Queue service run by [RQ](https://python-rq.org/). This is a very simple queue system based on redis.
3. [Redis](https://redis.io/). Used as a DB by the backend and as a queue storage by RQ.

Heres a basic architecture diagram.
![BeforeAfter]({{ site.url }}/assets/images/architecture.png)

Theres also [caddy](https://caddy.community/) run as a web server to route requests. The only big modification here is theres a config change to only allow up to 50mb for uploads. This is just so the server disk doesnt get filled up.

The three parts were hooked up using docker compose and run on a $1/month VPS. 

The basic flow is,
1. User uploads a file to be converted
2. Backend verifies the file and adds to a work queue with the location of the file and the url where it will be available
3. Backend redirects the user to a waiting page with an idenfifier where the user can wait for the file to be converted. The page will auto update when the file has been converted
4. The worker gets messages from the queue and runs kcc and converts the file. After it is done, marks the file as complete in redis.
5. At the identifier url, the page gets updated with the file and the user is able to downloaded the converted file.

If you want to try it out, send me an email and I can send you a link for you to try!