---
layout: post
title: "Using 'on' and 'off' events in App Cloud"
date: 2012-06-27 11:04
comments: true
categories: [App Cloud, JavaScript, jQuery]
---

The latest version of the [App Cloud][1] SDK includes jQuery 1.7, which
introduces new methods for handling events.

## Background

Prior to version 1.7, jQuery gave us a handful of ways to handle events.
You're probably familiar with the `bind` method:

    $("li").bind("click", function (evt) {
        // do stuff
    });

Above, we're _binding_ an anonymous callback function to every _li_ element in
the document. The callback function has one argument (an object) that contains
all the properties of the captured event. It's simply a shorthand for the
following:

    var elems = document.querySelectorAll("li");

    for (var i = 0; i < elems.length; i++) {
        elems[i].addEventListener("click", function (evt) {
            // do stuff
        });
    }

The jQuery version is nicer, don't you think?

The `bind` method works on elements that already exist in the document. But what
if the elements don't exist yet? Enter the `live` method:

    $("li").live("click", function (evt) {
        // do stuff
    });

The `live` method works on matched elements now or in the future by attaching
a single event listener to the document root element and then inspecting the
event data to determine which specific handlers to trigger. Pretty handy. The
`delegate` method works in a similar fashion, although you can specify a scope:

    $("ul").delegate("li", "click", function (evt) {
        // do stuff
    });

Each of these methods has a corresponding function to remove event listeners:
_bind_ and _unbind_, _live_ and _die_, _delegate_ and _undelegate_.

## New in jQuery 1.7

In jQuery 1.7, all the above methods are replaced with `on` and `off`. There
are two ways to use `on`:

    $("#dataTable tbody tr").on("tap", function (evt) {
        // do stuff
    });

    $("#dataTable tbody").on("tap", "tr", function (evt) {
        // do stuff
    });

The first technique is like using `bind`; the second technique is like using
`delegate` and is more efficient when working with large DOM trees.

See the [jQuery docs][2] for a complete rundown.

[1]: http://appcloud.brightcove.com
[2]: http://docs.jquery.com