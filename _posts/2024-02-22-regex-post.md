---
layout: post
title:  "Sift Through Chaos: A Regex Tutorial" 
date: 2024-02-22
description: Learning how to use regex for python and data collection.   
image: "/assets/img/RegExLogo.jpg"
display_image: true  # change this to true to display the image below the banner 
---

### So what's all this then?

When I was a lad, I had a cat named "Howard". This cat taught a lesson I will never forget. She told me:

> Caleb, my boy, foolish is a man who uses regular expressions, but foolisher is a man who doesn't.

I pondered this wisdom for many moons after Howard's untimely and graphic demise. After struggleing with her words, I grew to know the truth of the world at large. And so today I will teach you all how to use regex.


### What is Regex?

At it's core, regular experessions(regex) is a method of identifing patterns inside a string. Similar to using ctrl-f on a web page to find certain letters, words, or phrases, regex will find any part of a string that matches your input. Unlike using the find feature, regex is more robust and maluable.

For example, if I wanted to find the words 'bat' or 'cat' in an article, I could make two seperate searches for `bat` and `cat` individually. Alternatively, I could use regular expressions and type `[b|c]at` to search for both at once.