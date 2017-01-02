---
layout: post
title: Learning Lua
date: '2017-01-02T12:35:57+09:00'
tags:
- lua
- advent of code
---
A friend of mine on IRC, haste, told me about Advent of Code recently. Its a coding challenge in the style of an advent calendar, where you get a small problem to do every day in december until christmas. I wanted to learn Lua so I took the chance and started doing the challenges in lua. I have my solutions up on https://github.com/jinpark/adventofcode2016

A few things I learned

1. Lua does not have much of a standard library
2. Arrays and dicts are the same data structure
3. Penlight is a great package for the great standard libraries I got used to during python development.
4. The REPL (pre 5.3) does not take input as expressions, but as statemtents. This means that `> 10 + 20` does not return 30 but returns 
`stdin:1: unexpected symbol near '10'` instead
5. Lua starts indicies at 1 instead of 0. First, this was a bit of a mindfuck but as I got used to it, it made sense how easy it was to figure about indecies in arrays. This does make negative indexes (something that is not available in standard lua) a bit difficult.

Overall, writing lua forced me to rethink the way I write code and be a little bit smarter about how I use the standard library. Having such a limited pool of functions I can pull from made me think about what my code is actually doing and be aware of the chokepoints hidden in my code.
