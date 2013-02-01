---
layout: post
title: "Caching data feeds in App Cloud"
date: 2012-01-31 16:17
comments: true
categories: [App Cloud, JavaScript]
---

Caching data with `bc.core.cache()` will improve the performance and
"stickiness" of your app. Here are three reasons to do it:

## Speed up your app

Seconds matter, especially in mobile phone apps. While you're waiting for new
data to load from the server, you can display cached data. Often, the data
will be the same. In any case, you're giving the user something to process
instead of just a spinning wheel.

## Save bandwidth

Bandwidth isn't free. It costs time and money—especially for users without
unlimited data plans. Lend a hand and don't load data more frequently than is
absolutely necessary. If the data is relatively permanent, load it once and
cache it for a length of time (a day, a week, or more) before requesting it
again. You can use timestamps (in the cache!) for this purpose. Let's say
you're pulling down a list of instructional videos that rarely changes:

    var loaded_at = bc.core.cache("video_feed_loaded_at") || 0; // defaults to 0
    var time_now = new Date().getTime();
    var interval = 1000 * 60 * 60 * 24 * 3; // 3 days

    // if the cached data is older than 3 days
    if (time_now - loaded_at > interval) {
        // load new data from server and overwrite the cached data
        bc.core.getData("videos",
            function (data) {
                bc.core.cache("video_feed", data);
                bc.core.cache("video_feed_loaded_at", new Date().getTime());
                displayVideos();
            },
            function (error) {
                // oops
            }
        );
    }
    // else show cached data
    else {
        displayVideos();
    }

    function displayVideos() {
        var feed = bc.core.cache("video_feed");
        // do stuff
    }

Above, we're loading new data only if the cached data is empty (i.e. it has
never been loaded) or if the cached data is more than three days old.

Note, you can always provide a "refresh" button for users to update data on
their own. And sometimes it's a good idea to display a "last updated" date
alongside the results.

## Save user preferences and other metadata

The cache is a great way to store preferences and other values that are
specific to a particular user on a particular device. For example, you can
save the user's preferred display mode:

    bc.core.cache("user_pref_display_mode", "grid");

Or, you can store a list of recently viewed articles, or favorites, by ID. I
wrote some helper functions for this purpose:

    // cache a "favorite" value in an array with the given key
    // e.g. saveFavorite("fruits", "apple")
    function saveFavorite(key, val) {
        var favorites = bc.core.cache(key) || [];

        if (favorites.indexOf(val) === -1) {
            favorites.push(val);
        }

        bc.core.cache(key, favorites);
    };

    // delete a "favorite" value from a cached array with the given key
    // e.g. deleteFavorite("fruits", "apple")
    function deleteFavorite(key, val) {
        var favorites = bc.core.cache(key) || [];
        var idx = favorites.indexOf(val);

        if (idx > -1) {
            favorites.splice(idx, 1);
            bc.core.cache(key, favorites);
        }
    };

    // determine if a value is contained in a list of favorites
    // e.g. isFavorite("fruits", "apple")
    function isFavorite(key, val) {
        var favorites = bc.core.cache(key) || [];

        return favorites.indexOf(val) > -1;
    };

The function `bc.core.cache()` is actually a wrapper for 
[Local Storage][1]—sometimes called "cookies on steroids." As you've seen, 
it's a simple yet invaluable way to add state to your applications.

[1]: http://coding.smashingmagazine.com/2010/10/11/local-storage-and-how-to-use-it/