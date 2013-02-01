---
layout: post
title: "Creating a reading list in App Cloud"
date: 2012-02-10 17:03
comments: true
categories: [App Cloud, JavaScript]
---

The function `bc.core.cache()` is great for all kinds of things: saving user
preferences, saving application state, or saving "favorites," as in a reading
list.

Here are some functions for maintaining a list of "favorites" in the cache. In
this case, the favorites are news articles selected by the user. Each article
is represented by a JavaScript object with a unique ID:

    // get the favorites from cache, or return an empty array
    function getFavorites() {
        return bc.core.cache("favorites") || [];
    }

    // overwrite the favorites in cache
    function setFavorites(favorites) {
        bc.core.cache("favorites", favorites);
    }

    // determine if an article is a favorite (by article ID)
    function isFavorite(articleId) {
        var favorites = getFavorites();

        for (var i in favorites) {
            if (favorites[i].articleId === articleId) {
                return true;
            }
        }

        return false;
    }

    // save an article as a favorite (by article ID)
    function addToFavorites(articleId) {
        var favorites = getFavorites();

        if (!isFavorite(articleId)) {
            favorites.push(getArticle(articleId));
        }

        setFavorites(favorites);
    }

    // remove an article from favorites (by article ID)
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

To see this in action, check out the "reading list" demo in the
[App Cloud Demos][1] repository on Brightcove Open Source.

[1]: https://github.com/BrightcoveOS/App-Cloud-Demos