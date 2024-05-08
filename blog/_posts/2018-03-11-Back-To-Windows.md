---
layout: post
title: Back to Windows?
date: '2018-03-11T01:50:29+09:00'
tags:
- mac
- windows
- Linux
- WSL
- Windows Subsystem for Linux
- Ubuntu
---
I've switched jobs recently and needed a new laptop for work, which includes working on a React Native app.

I dropped my personal 2014 Macbook Pro a little while ago and broke the screen, so I've been using it as a desktop, leaving me with only my 2011 Macbook Air. While the Air is still working great, not counting the low battery life, it can't handle runnng the React Native packager and Android Emulator without choking. For a little while, I've been using my main phone (a Xiaomi Redmi 3S Prime) to develop the app, but it is a pain to having to check another device to do my work.

I've been pretty disappointed with the new Macbook Pros, the increased prices as well as the reduced functionality, so I was looking at other similar high end windows/linux laptops (Dell XPS 13, Thinkpad X1 Carbon, etc). While searching, I came across [this youtube video](https://www.youtube.com/watch?v=BlMKftsnfWE) where it showed off the Acer Aspire 5 as a budget gaming PC, coming in at around $600 USD, with a 8th gen i5 and discrete graphics. That came to about 1/3rd of the price of a Macbook Pro 15 while having similar specs. I did some research online to see if this was available in Korea and I found a similar Acer model for about the same price but with an IPS screen instead of a TN screen, 4GB of RAM instead of 8, and 128GB of storage instead of 256. I found a 8GB RAM stick for about $75 USD and bought the whole system for about $675 USD. While this isin't pocket change, this was significantly cheaper than the other options I was looking at, and if it was no good, I could at least use it as a gaming computer!

My goals with this computer was that I should be able to setup Windows, get the WSL working and setup React Native along with the Android emulator. Setting up Windows and getting the WSL working was a breeze, installing node, npm and yarn was slightly annoying due to permissions issues but I had it working pretty quickly. The difficult part that I did not expect was getting React Native in WSL to work with the emulator in Windows. Luckily for me, someone else had the same problem as me in [Stack Overflow](https://stackoverflow.com/questions/42614347/running-react-native-in-wsl-with-the-emulator-running-directly-in-windows) and pointed out that you can run the packager in WSL and install the debug APK manually through Powershell. This worked pretty well since you only need to install the APK once in the emulator. Installing and setting up the emulator was overly convoluted (installing Android Studio, installing java, setting up a new project, deleting the project because it was using the wrong sdk), but with help from SO and google, it got done.

My Windows setup is now, WSL for git and running node/react-native-cli, Visual Studio Code as an editor, and Android Studio to run the emulator. I'm still working on getting fish to be my default shell. 

UPDATE: So one problem I ran into is that the Android Emulator (bundled into Android Studio) requires Hyper-V to be turned off, while Docker for Windows requires it to be turned on. I was lucky enough to be able to run what I needed to run on docker locally but I can see this being a real problem later on. I found that you can use [Visual Studio Android Emulator](vhttps://www.visualstudio.com/vs/msft-android-emulator/) as an alternative emulator that works with Hyper-V but it does seem slower.