---
layout: post
title: Pokemon Go and OCR
date: '2016-07-26T12:35:57+09:00'
tags:
- pokemon go
- ocr
---

I wanted to make a quick and easy webapp for Pokemon Go and I ended up stealing my friend [Trond](http://github.com/haste)'s idea for his ingress [http://tie.rs/](http://tie.rs/) stats app. 

This simple webapp takes in a screenshot from your pokemon team page and then parses it and creates a sharable webpaage for you to show off your team. The current implementation is at [pokemon-go-team.herokuapp.com](https://pokemon-go-team.herokuapp.com) and you can see what it outputs [here](https://pokemon-go-team.herokuapp.com/team/b4f08b6090/)


![](https://forestryio.s3-us-west-2.amazonaws.com/wdn0ioiolknhfq/forestryio/images/andrew.jpg)
*Example Team Screenshot*



Since API access is still illegal for Pokemon GO, the only "legal" way to access team data is if the user sends it voluntarily. The front end takes in the screenshot and sends it to the backend to handle it.

The app does a few things to process the screenshot.


1. The screenshot's height and width are measured through [pillow](https://python-pillow.org/).

![](https://forestryio.s3-us-west-2.amazonaws.com/wdn0ioiolknhfq/forestryio/images/pokemononly.png)
2. The top portion of the screen (status bar, tabs) are removed so just the pokemon are shown.

![](https://forestryio.s3-us-west-2.amazonaws.com/wdn0ioiolknhfq/forestryio/images/row.png)
3. The pokemon section is split into single rows. Currently, we're just taking the top 6 pokemon, so 2 rows.

![](https://forestryio.s3-us-west-2.amazonaws.com/wdn0ioiolknhfq/forestryio/images/dodrio.png)  
4. The row is split into 3 columns for each pokemon while removing 15% of the width from each side to remove unnecessary scroll bars.  
5. Each pokemon section is cut horizontally into 3 sections. Top area for the name, bottom area for the CP and the middle for the image which we discard.  
![](https://forestryio.s3-us-west-2.amazonaws.com/wdn0ioiolknhfq/forestryio/images/name.png)  
6. The top area with just the name is OCR-ed.  
![](https://forestryio.s3-us-west-2.amazonaws.com/wdn0ioiolknhfq/forestryio/images/cp.png)  
7. The bottom area with the CP is OCR-ed and the "CP" part is discarded.  

After OCR-ing, we end up with a hash for each pokemon and their cp. We send that info to the front end and allow the user to make changes, since the OCR might have been incorrect OR the pokemon name was actually just a nickname. I'm using [pokeapi](https://pokeapi.co/) to get pokemon data and I scraped the pokemon move data from [serebii](http://serebii.net/pokemongo/moves.shtml).

The technologies used are flask for the backend web portion, pillow for the image cropping and manipulation, pyocr and pytesseract for OCR, redis for a simple database, jquery and semantic-ui for the frontend.

At the end, you get something like [this](https://pokemon-go-team.herokuapp.com/team/b4f08b6090/) which you can share with others.
