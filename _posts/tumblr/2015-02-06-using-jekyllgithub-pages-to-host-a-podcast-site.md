---
layout: post
title: Using jekyll/github-pages to host a podcast site
date: '2015-02-06T06:31:43+09:00'
tags:
- podcast
- jekyll
- github
tumblr_url: http://blog.jinpark.net/post/110243175622/using-jekyllgithub-pages-to-host-a-podcast-site
---
Two of my friends (Ahnmin and Bobby) at work started making a podcast together called Something Sunshine and like any podcast, they needed a website. Since this was just a fun project for them, I wanted to make sure that they did not have to pay for anything.

I was thinking of what would be easy and free and my first thought went to meteor, a new js framework that I was learning. It reminded me of rails a lot due to its convention over configuration mindset and its ease of use. I started setting that up but realized that I might be over engineering this. What they needed was a simple cms where they can upload a “post” or a podcast episode and some metadata. Meteor was for a full application. Definitely not the right usecase. Time to think of a simpler alternative.

At work (DramaFever), we are trying to move our flatpages (embedable html pages usually used for marketing), into github so there could be at least some semblance of a code review when our designers upload their new designs.

I wanted to take that same idea and use it for the podcast site.

Jekyll is a very simple blog platform written in ruby that is hostable (for free) on github pages that uses simple markdown files as blog posts. It also allows simple metadata using YAML’s front matter. It’s not as nice as a full CMS like wordpress, but its very lightweight and easy to learn.

I set up a simple site using fullpage.js and, since the podcast authors wanted to use soundcloud, a very simple soundcloud embed system with a few event handlers so we can keep track of some basic stats through google analytics. I also saw that others are using jekyll for podcasting and have even made itunes compatible rss feeds through jekylls templating service.

I haven’t opensourced it yet due to it being in progress and theres a lot of application specific things that are in the code. After I pull that out into its own settings file, it’ll be out in the wild for anyone to use :)

Seriously, check out Something Sunshine. It’s a podcast about movies, video games, music and anything else that comes to mind. They are great hosts and extremely fun to listen to!

As an update (May 23 2015), We ended up moving to django and using their admin to handle everything. This was more of a monetary thing than a tech thing. We were using soundcloud to host our files but were limited to a 3 hour max limit for the free plan. We could have moved it to the repo itself but that would have been fairly complicated for our non technical podcast makers. I’ve open sourced the repo but its pretty dirty and I haven’t gotten around to cleaning it up
