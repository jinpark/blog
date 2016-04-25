---
layout: post
title: Docker and Tutum
date: '2015-04-06T01:50:29+09:00'
tags:
- docker
- python
- tutum
tumblr_url: http://blog.jinpark.net/post/115645836957/docker-and-tutum
---
Actually Docker, Docker Compose, Circle CI, Docker Hub, Digital Ocean, HAProxy and Tutum

To continue my education of best backend and ops practices, I decided to get better at understanding docker and use it in my own projects.

I’ve used docker and boot2docker at work but I never fully understood it completely and after one of my coworkers gave a presentation on docker compose, I felt like it was time that I started using docker for real and reduce my dependance on PAAS providers like heroku.

I followed the instructions on Real Python. One note is when you take the pre compose files, make sure that you delete or edit the .gitignore file since it prevents your changes to circle.yml and docker-compose files from being committed. I was fairly happy to see that the workflow, of using a CI service to test and then, on success, to “deploy” to another service (docker hub in this case), was the same as in my imageresizer service that I’ve written about previously.

The next step after that tutorial was deploying it onto a VPS. I took a look at the next step that they provided but I did not like the way they handled deployment. It used an api hook to call a shell script to update the container, which I felt was a bit weak. I took a look around and found Tutum. They are slightly abstracting the deployment steps of docker containers. It’s not as “fancy” as dokku but I felt it fit my use case. As time goes on I am pretty sure that I’ll start handing deployment myself but I want to make sure that I can get it working first with some help.

I changed my imageresizer code to make it run as a docker container here and after going through circle ci, it gets saved as a docker imge here.

After deploying it on dokku and fooling around with exposing the right ports, it was working great. The next step was using some type of reverse proxy to host and expose multiple docker containers on one VPS. Tutum provides a HAProxy container that does this for you “automagically”. Except that the magic part needs to be worked on a bit.

I spent some time figuring out how to get this working after following the instructions. What I had to do to get this working was to add a VIRTUAL_HOST env variable within each of my services with the url of what I wanted to route, and also change the BACKEND_PORTS env on the haproxy service to what the linked ports are for your services. I think Tutum is supposed to handle this automatically but I don’t see this happening.

You can see this working by going to `http://images1.jinpark.net/http://i.imgur.com/6GSvBbn.jpg/?rwidth=200` (currently down) which is the image resizer service and at `http://hello.jinpark.net` (also down) which is the standard hello world tutum container. Both these containers are hosted on the same Digital Ocean VPS and are routed through HAProxy which was handled by Tutum.
