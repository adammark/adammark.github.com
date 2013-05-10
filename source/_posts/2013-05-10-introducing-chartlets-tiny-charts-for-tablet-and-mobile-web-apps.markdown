---
layout: post
title: "Introducing Chartlets: Tiny charts for tablet and mobile web apps"
date: 2013-05-10 14:03
comments: true
categories: [Chartlets, JavaScript]
---

Choosing the right tool (or _tools_) for data visualization suddenly got complicated.
Flash is out, [SVG][2] and [Canvas][3] are in, and a [mess of libraries][1] have 
made it possible to offload expensive rendering tasks from the server to the client.

My favorite libraries are [D3.js][4] for SVG and [Chart.js][5] for Canvas. D3.js is 
particularly sophisticated and makes few assumptions about how to render data; its
primary goal is to bind data to DOM elements and help manipulate elements. Chart.js
is great for rendering simple, static charts.

Most libraries are biased toward _big_ presentations. I went the other way when I 
created [Chartlets][6], a library for making minimalist charts for mobile and tablet 
web apps:

![](/images/work/chartlets-samples-640x480.png)

Not only are Chartlets small, the library itself weighs in at under 3K. And the API
is simple by design, requiring no programming knowledge to render a basic chart.
Chartlets can be defined entirely in HTML:

    <canvas class="chartlet" width="65" height="65" 
      data-type="pie" data-sets="[1 2 3 4 5]" data-opts="theme:money"></canvas>

Check out the full docs and examples at [chartlets.com][6].

[1]: http://selection.datavisualization.ch/
[2]: https://developer.mozilla.org/en-US/docs/SVG
[3]: https://developer.mozilla.org/en-US/docs/HTML/Canvas/Tutorial
[4]: http://d3js.org/
[5]: http://chartjs.org
[6]: http://chartlets.com