---
layout: post
#title: Using KCC (Kindle Comic Converter) with an M1 Mac
date: '2021-05-04T01:50:29+09:00'
tags:
  - kindle
  - manga
---
I'm a big fan of [Kindle Comic Converter](https://kcc.iosphe.re/). Its a python GUI app that converts epub, png, jpg, etc. files that make up a comic or manga, into a `.mobi` file that works with the amazon kindle. It also intelligently supports upscaling and cover generation. If you have an epub manga that you got off the back of a truck or more likely, one rented from overdrive/library but in epub format that you want to read on your kindle, I would recommend that you try out KCC.

The basic feature set is
- converts epub, png, etc into a mobi file for the kindle
- can remove margins to maximize screen space
- can generate cover art for the mobi file so the book on the kindle has the correct cover
- 

At the heart of KCC is KindleGen, an old utility command line program provided by Amazon for publishers to help them create ebooks to sell on Amazon. It is currently [discontinued](https://www.amazon.com/gp/feature.html?ie=UTF8&docId=1000765211) which makes KCC mostly unusable if you want to create mobi files for older kindles. Even if you get an old download of KindleGen, it is only a 32-bit executable, which makes it unusable on Mac OS Catalina and above. Amazon now provides [kindle previewer](https://www.amazon.com/gp/feature.html?ie=UTF8&docId=1000765261) which also mostly does the [same (and more)](https://github.com/ciromattia/kcc/issues/371#issuecomment-713816833) as KindleGen but in a nicer GUI. But KindlePreviewer is not made specifically for manga/comics so KCC still has a leg up. Surprisingly, at the core of Kindle Previewer is an updated version of KindleGen. If you look in the application bundle for Kindle Previewer for 64-bit Mac, there exists a 64-bit version of KindleGen. This was discovered on a forum [here](https://www.literatureandlatte.com/forum/viewtopic.php?p=284621#p284621). There also exists a [github repo](https://github.com/andyljones/kindlegen-64) where someone has done this for you.

After you get KindleGen, you can point KCC to it so it can use it and run KCC as a rosetta (emulated) app and you should be able to 
