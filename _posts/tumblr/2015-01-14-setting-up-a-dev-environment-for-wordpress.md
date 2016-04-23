---
layout: post
title: Setting up a dev environment for wordpress
date: '2015-01-14T03:49:00+09:00'
tags:
- wordpress
- server
tumblr_url: http://blog.jinpark.net/post/108063835707/setting-up-a-dev-environment-for-wordpress
---
This might be extremely boring for anyone who maintains servers as it is the most basic level stuff that you guys probably know :P

I’ve been helping a friend monitor and update her wordpress blog that gets a decent amount of traffic.

She wanted to do some large changes to her blog but didn’t want any downtime. So, the next step was to get a quick dev environment up so that she could test her changes and get a feel of how things changed.

Cloudatcost is a Canada based provider of cheap VPS services. They have a $35/lifetime plan for a low end VPS that I’m using. Reviews say they suck, especially regarding uptime, but for something like this where uptime is not important. I feel like this was the right choice.

I installed ubuntu 14.04 x64 and started using this digital ocean tutorial  to get started. I was using this plugin. This plugin needed apache/php/mysql installed but not wordpress.

So after everything was installed on the dev server and the backup/installation files were copied over to the html folder on the machine. Before you install, you should modify the permissions of the html folder so php could write to it. After that’s done, you also need to enable mod_rewrite with this command

 sudo a2enmod rewrite 


add

<Directory /var/www/html>
AllowOverride All
Order allow,deny
</Directory>


to your /etc/apache2/sites-available/000-default.conf file and then restart apache with

sudo service apache2 restart 


This allows the .htaccess file to be created by wordpress so you can modify your permalinks.  Most of this is written here

Run through the installation and check your wp-config.php file to check for references to your old domain. I had to remove the caching plugin and reenable to get it to work.

Now everything should work!
