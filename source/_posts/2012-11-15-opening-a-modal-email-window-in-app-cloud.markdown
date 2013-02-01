---
layout: post
title: "Opening a modal email window in App Cloud"
date: 2012-11-15 14:56
comments: true
categories: [App Cloud, JavaScript]
---

The latest version of the [App Cloud][2] SDK (1.12) introduces a new device
method for launching a modal email window inside an app. (Previously, the only
way to launch a native email client was through a "mailto" link, which bounced
users out of the app. Boo.) Here's how to do it:

    // all properties optional
    var options = {
        toRecipients: "john@example.com, jane@example.com",
        subject: "Check it out!",
        body: "I found this interesting: http://www.example.com/"
    };

    // fired when the email is sent
    var successCallback = function () {
        // yay!
    };

    // fired if the user cancels
    var errorCallback = function (error) {
        // boo!
    };

    // open the modal
    bc.device.modalEmail.composeEmail(successCallback, errorCallback, options);

Of course, in your own code you'd have to pass some real data into the options
object. Check out the [API docs][1] for a full rundown.

[1]: http://docs.brightcove.com/en/app-cloud-api/core/symbols/bc.device.modalEmail.html
[2]: http://appcloud.brightcove.com