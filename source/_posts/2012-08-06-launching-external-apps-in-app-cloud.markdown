---
layout: post
title: "Launching external apps in App Cloud"
date: 2012-08-06 15:44
comments: true
categories: [App Cloud, JavaScript]
---

Sometimes it's necessary to launch an external app from within your own app.
_After all, your app can't do everything!_ In [App Cloud][1], it's easy to do
with the device method `bc.device.openURI()`.

Say you want to open an external web browser whenever a user taps a button:

    $("#exampleButton").on("tap", function (evt) {
        // both callback functions are optional
        bc.device.openURI("http://www.example.com", onSuccess, onError);
    });

Easy enough! But what if you have many buttons, each leading to a different
URI? Consider embedding each URI in a data attribute:

    <button data-href="http://www.example.com">Open me</button>
    <button data-href="http://www.example.net">Me too!</button>

Then you can listen for a tap event on any element having a "data-href"
attribute and extract the URI from that element:

    $("[data-href]").on("tap", function (evt) {
        var uri = this.getAttribute("data-href");
        bc.device.openURI(uri, onSuccess, onError);
    });

## Special cases

In some cases, iOS uses specific apps to handle special types of URLs. For
example, any URL beginning with "http://maps.google.com" opens in the Maps
app:

![iOS screen shot](/images/blog/app-cloud-open-uri-ios.jpg)

Android may present the user with several options in order to determine the
"intent" of the action:

![Android screen shot](/images/blog/app-cloud-open-uri-android.jpg)

## Using modal windows

If you're simply opening a web page, you might want to open it modally instead
of bouncing the user out of your app. Just set "modalWebBrowser" to true in
the device call:

    bc.device.openURI(url, onSuccess, onError, { modalWebBrowser: true });

You can also use links to accomplish the same thing without JavaScript:

    <a href="http://www.example.com">For example ...</a>

[1]: http://appcloud.brightcove.com