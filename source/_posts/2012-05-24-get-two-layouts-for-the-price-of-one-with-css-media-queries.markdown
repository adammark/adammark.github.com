---
layout: post
title: "Get two layouts for the price of one with CSS Media Queries"
date: 2012-05-24 11:25
comments: true
categories: [App Cloud, Design]
---

![Screen Shot](/images/blog/app-cloud-orientation.jpg)

Some [App Cloud][3] developers have asked me how to change the layout of a
view depending on the device's orientation. The simplest way—and this is
really very simple—is to use [Media Queries][1]:

    @media all and (orientation: portrait) {
        /* CSS rules here */
    }

    @media all and (orientation: landscape) {
        /* CSS rules here */
    }

For example, let's say you want to change the body color from red to green
when the user rotates the device from portrait to landscape:

    @media all and (orientation: portrait) {
        body {
            color: red;
        }
    }
    @media all and (orientation: landscape) {
        body {
            color: green;
        }
    }

Add the above code to your stylesheet and see what happens. (You can test it
in your Webbrowser by resizing the window.)

It's not necessary to put all your styles inside the media queries—just the
styles that are specific to portrait or landscape mode.

Combine Media Queries with the [Flexible Box Model][2] and now you're cooking
with gas!

Two notes: First, you must allow for orientation changes in the SDK by calling
`bc.device.setAutoRotateDirections(["all"])`. Second, CSS rules can only
affect the layout, not the behavior, of your app. You can listen for a
`vieworientationchange` event if you need to perform some action when the user
rotates the device.

[1]: https://www.google.com/search?q=css3+media+queries+tutorial
[2]: http://www.html5rocks.com/en/tutorials/flexbox/quick/
[3]: http://appcloud.brightcove.com