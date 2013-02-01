---
layout: post
title: "Working with arrays in App Cloud"
date: 2012-02-16 16:46
comments: true
categories: [App Cloud, JavaScript]
---

[App Cloud][1] apps are voracious consumers of JavaScript arrays, which carry
all kinds of data from server to client: news articles, photo gallery
metadata, a list of places near a user's location, and even tweets. You're
probably familiar with the two basic techniques for iterating over arrays:

    for (var i = 0; i < stuff.length; i++) {
        ...
    }

and

    for (var i in stuff) {
        ...
    }

Now comes another:

    stuff.forEach(function (value, index, array) {
        ...
    });

Yeah, you read that right. And it doesn't use jQuery or any other syntactic
sugar. Here's a fuller example:

    var fruits = ["apple", "banana", "cherry"];

    fruits.forEach(function (value, index, array) {
        console.log(value, index, arr);
    });

Run the above code in your browser to see the output—then feel free to use
this technique in your App Cloud app.

There are some other native JavaScript methods that might look new to you:
`every()`, `filter()`, `map()` and `some()`. Read all about them in the 
[MDN docs][2].

[1]: http://appcloud.brightcove.com
[2]: https://developer.mozilla.org/en/New_in_JavaScript_1.6
