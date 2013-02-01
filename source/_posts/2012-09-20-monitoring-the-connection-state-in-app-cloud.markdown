---
layout: post
title: "Monitoring the connection state in App Cloud"
date: 2012-09-20 12:00
comments: true
categories: [App Cloud, JavaScript]
---

The latest version of the [App Cloud][1] SDK (1.11) introduces a new type of
event for monitoring whether the user is online or offline. It's a snap to
use:

    $(bc).on("connectionstatechange", function(evt, data) {
        if (data.online) {
            // do something
        }
        else {
            // do something else
        }
    });

Now you can take appropriate action when a user's connection goes in or out.
For example, say you want to show a status indicator:

    function displayStatusIndicator(online) {
        // show or hide the indicator
    }

    $(bc).on("connectionstatechange", function(evt, data) {
        displayStatusIndicator(data.online);
    });

Sometimes it's necessary to check the connection status before performing a
particular action. For this you can look to the `bc.context` object:

    $(bc).on("init", function (evt) {
        if (bc.context.online) {
            loadNews();
        }
        else {
            displayCachedNews();
            showOfflineMessage();
        }
    });

Together, the `connectionstatechange` event and `bc.context.online` property
can help you handle network failures gracefully.

[1]: http://appcloud.brightcove.com