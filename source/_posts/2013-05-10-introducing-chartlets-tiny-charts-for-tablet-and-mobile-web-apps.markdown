---
layout: post
title: "Introducing Chartlets: Tiny charts for tablet and mobile web apps"
date: 2013-05-10 14:03
comments: true
categories: [Chartlets, JavaScript]
---

I just put the finishing touches on [Chartlets][1], a library for making 
tiny charts for mobile and tablet web apps:

![](/images/work/chartlets-samples-640x480.png)

While most data visualization libraries are biased toward _big_ displays, 
Chartlets assumes the opposite. Not only are Chartlets small, the library 
itself weighs in at under 3K. And the API is drop-dead simple, requiring 
no programming knowledge to render a basic chart. Chartlets can be defined 
entirely in HTML:

    <canvas class="chartlet" width="65" height="65" 
      data-type="pie" data-sets="[1 2 3 4 5]" data-opts="theme:money"></canvas>

Check out the full docs and examples at [chartlets.com][1].

[1]: http://chartlets.com