---
layout: post
title: "Lazy loading your views in App Cloud"
date: 2011-11-17 16:12
comments: true
categories: [App Cloud, JavaScript]
---

"Lazy loading" doesn't mean you're lazy. It's simply a technique for deferring
an operation until it's absolutely necessary.

If your template has multiple views, you should consider building up each view
when the user enters it—and not before. You'll save memory and improve the
performance of your app by preventing all your business logic across all your
views from running at the same time.

In the following example from my "Map" view (map.html), the function `MapView`
is responsible for loading and rendering the dynamic content on the page:

    var view;

    $(bc).on("viewfocus", function (evt) {
        if (!view) {
            view = new MapView();
            view.init();
        }
    });

By listening for a `"viewfocus"` event, I can wait to create a MapView
instance until the moment the user enters the view. This way, I avoid eating
up system resources—and slowing down the user experience—while the user is off
playing in another view.

(And while the new content is loading, I show cached content alongside a "Loading ..."
message.)
