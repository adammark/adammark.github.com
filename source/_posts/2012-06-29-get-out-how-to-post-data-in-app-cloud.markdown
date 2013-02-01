---
layout: post
title: "GET out! How to POST data in App Cloud"
date: 2012-06-29 11:21
comments: true
categories: [App Cloud, JavaScript]
---

The [App Cloud][1] SDK provides two device methods for exchanging data with
remote services. You're probably familiar with the first one:

    bc.device.fetchContentsOfURL(url, successCallback, errorCallback)

This method makes a cross-domain GET request, AJAX-style, to a remote URL. You
might use it to pull down some tweets:

    var url = "http://api.twitter.com/1/statuses/user_timeline.json?id=@adammark75";

    var handleData = function (data) {
        var tweets = JSON.parse(data);

        displayTweets(tweets);
    };

    var handleError = function (error) {
        bc.device.alert("Oops! " + error.errorMessage);
    };

    bc.device.fetchContentsOfURL(url, handleData, handleError);

The second method works the same way, except it makes a POST request:

    bc.device.postDataToURL(url, successCallback, errorCallback, options)

You might use it to send credentials to an authentication service:

    var url = "https://example.com/login";

    var options = {
        data: {
            "username": "boba",
            "password": "fett"
        }
    };

    var handleData = function (data) {
        var response = JSON.parse(data);

        if (response.authorized) {
            permitUser();
        }
        else {
            rejectUser(response.failureCode);
        }
    };

    var handleError = function (error) {
        bc.device.alert("Oops! " + error.errorMessage);
    };

    bc.device.postDataToURL(url, handleData, handleError, options);

With these two device methods, you can access any REST service, AJAX-style!

[1]: http://appcloud.brightcove.com