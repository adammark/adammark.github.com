---
layout: post
title: "Introducing Markup.js: Powerful JavaScript templates"
date: 2011-08-24 16:01
comments: true
categories: [JavaScript, Markup.js]
---

When I started making [App Cloud][1] apps, I thought I could benefit from
using a JavaScript templating system. So I toyed around with two popular
frameworks, [Mustache][2] and [jQuery Templates][2]. Unfortunately I didn't
like either. I found Mustache to be too simplistic (it prides itself on being
_logicless_), while jQuery Templates required me to use jQuery.

So I decided to write my own templating system with the following goals:

* It should have an elegant syntax with minimal punctuation
* It should be fast and lightweight
* It should have no library dependencies
* It should not require a browser or DOM
* It should be flexible enough to support internationalization (i18n) tasks

The result: [Markup.js][2]. Weighing in at only 1.7KB after minification and
gzipping, it includes a simple yet powerful expression language for
transforming structured data into HTML and other text formats. So far, I'm
loving it.

[1]: http://appcloud.brightcove.com
[2]: https://github.com/adammark/Markup.js