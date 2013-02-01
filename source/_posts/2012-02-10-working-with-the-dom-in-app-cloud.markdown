---
layout: post
title: "Working with the DOM in App Cloud"
date: 2012-02-10 16:09
comments: true
categories: [App Cloud, JavaScript]
---

Apps are full of lists—articles, videos, events, and so on—and these lists are
often created dynamically with JavaScript. Say you're creating a list of news
articles. Your HTML might begin like this:

    <ul id="articles">

    </ul>

How should you fill the empty `<ul> `with content? There are two basic
approaches:

### The BAD way

    var elem = document.getElementById("articles");

    for (var i = 0; i < data.length; i++) {
        elem.innerHTML += "<li>" + data[i].title + "</li>";
    }

### The GOOD way

    var elem = document.getElementById("articles");
    var str = "";

    for (var i = 0; i < data.length; i++) {
        str += "<li>" + data[i].title + "</li>";
    }

    elem.innerHTML = str;

What's the difference? The _bad_ technique modifies the DOM over and over
again, causing the web view to repaint and reflow the document many times.
What a drag!

The _good_ technique builds up a string in memory, then injects it into the
DOM once and only once. On mobile devices, this sort of optimization is
essential to creating speedy apps.

