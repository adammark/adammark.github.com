---
layout: post
title: "Discovering the cache in App Cloud"
date: 2012-03-14 17:09
comments: true
categories: [App Cloud, JavaScript]
---

![Aaargh.](/images/blog/app-cloud-treasure.jpg)

If you've never the cache in [App Cloud][1], you'll feel like you just
discovered a buried treasure. _Aaargh!_ Here are six ways to use the
cache in your app:

## 1. Save user preferences

If your app lets users select a display preference—for example, whether to
view items as a list or a grid—save the user's selection for next time:

    // set the preference
    bc.core.cache("USER_DISPLAY_MODE", "grid");

    // get the preference, defaulting to "list"
    var displayMode = bc.core.cache("USER_DISPLAY_MODE") || "list";

## 2. Save user “favorites”

You can save entire objects in the cache. For example, an array of news
articles:

    // set favorites (an array) in the cache
    function setFavorites(favorites) {
        bc.core.cache("favorites", favorites);
    }

    // get favorites from the cache, or return an empty array
    function getFavorites() {
        return bc.core.cache("favorites") || [];
    }

    // add an article to favorites
    function addToFavorites(articleId) {
        var favorites = getFavorites();

        if (!isFavorite(articleId)) {
            favorites.push(getArticle(articleId));
        }

        setFavorites(favorites);
    }

    // remove an article from favorites
    function removeFromFavorites(articleId) {
        var favorites = getFavorites();

        for (var i in favorites) {
            if (favorites[i].articleId === articleId) {
                favorites.splice(i, 1);
                break;
            }
        }

        setFavorites(favorites);
    }

    // is an article already favorited?
    function isFavorite(articleId) {
        var favorites = getFavorites();

        for (var i in favorites) {
            if (favorites[i].articleId === articleId) {
                return true;
            }
        }

        return false;
    }

## 3. Save application state

Save the user some trouble by saving state—for example, the ID of the last
viewed article—and then restoring the UI to that state when the user returns.
You can use "viewblur" and "viewfocus" events to detect when a user comes and
goes:

    // save the last viewed article ID when user exits the view
    $(bc).bind("viewblur", function (evt) {
        bc.core.cache("LAST_VIEWED_ARTICLE_ID", articleId);
    });

    // restore the view if necessary when user re-enters
    $(bc).bind("viewfocus", function (evt) {
        var lastId = bc.core.cache("LAST_VIEWED_ARTICLE_ID");

        if (lastId) {
            // do stuff
        }
    });

## 4. Save data with a long shelf life

If you're working with data that has a long shelf life—for example, a blog
that gets updated once every week or two—you can pull the data from the cache
instead of hitting the server over and over again:

    var one_week = 7 * 24 * 60 * 60 * 1000;
    var time_saved = bc.core.cache("BLOG_DATA_LOADED_AT") || 0;
    var time_now = new Date().getTime();

    if (time_now - time_saved > one_week) {
        // load new data
        bc.core.getData("blog-feed", function (data) {
            // render blog with new data
            renderBlog(data);

            // update the data in cache
            bc.core.cache("blog-data", data);

            // update the timestamp in cache
            bc.core.cache("BLOG_DATA_LOADED_AT", time_now);
        });
    }
    else {
        // render blog with old data
        renderBlog(bc.core.cache("blog-data"));
    }

## 5. Show placeholder data

While you're loading new data, show old data as a placeholder. _Anything beats
a blank white screen:_

    var cachedData = bc.core.cache("blog-data") || [];

    renderBlog(cachedData);

    bc.core.getData("blog-feed", function (data) {
        renderBlog(data);
    });

## 6. Run your app in offline mode

Use the techniques described above to store non-critical data for offline use.
Your users will thank you!

Remember, unlike HTML5 Local Storage, `bc.core.cache()` takes care of
serializing and deserializing JavaScript objects for you.

[1]: http://appcloud.brightcove.com