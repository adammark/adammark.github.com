---
layout: post
title: "App Cloud and Kinvey: A one-two punch for content-centric, data-driven apps"
date: 2012-09-15 15:17
comments: true
categories: [App Cloud, Kinvey]
---

For many developers, [App Cloud][5] is a one-stop shop for all their
application needs. It's got a robust SDK and a _sweet suite_ of runtime cloud
services like image transcoding, data feed optimization, and cross-platform
push notifications. But no platform can do everything. While App Cloud is
primarily concerned with delivering content to apps, services like [Kinvey][1]
can help you manage the river of data that users might generate from inside
those apps.

Kinvey is remarkably easy to use. In just a few minutes, I created an account,
set up an "app" in the Kinvey console, created a "collection" of friends, and
started populating the collection from a few lines of JavaScript in my App
Cloud app.

![Kinvey Console](/images/blog/app-cloud-kinvey.jpg)

Adding a friend to my "friends" collection was a snap:

    function saveFriend(firstName, lastName) {
        var entity = new Kinvey.Entity({
            firstName: firstName,
            lastName: lastName
        }, "friends");

        entity.save({
            success: function(friend) {
                console.log(friend);
            },
            error: function(err) {
                console.log(err);
            }
        });
    }

Querying the collection was just as straightforward:

    function findFriendsByLastName(lastName) {
        var query = new Kinvey.Query();
        query.on("lastName").equal(lastName);

        var collection = new Kinvey.Collection("friends");
        collection.setQuery(query);

        collection.fetch({
            success: function (list) {
                list.forEach(function (item) {
                    console.log(item.attr.firstName, item.attr.lastName);
                });
            },
            error: function (err) {
                console.log(err)
            }
        });
    }

It was also a cinch to create new user accounts for permissioning purposes:

    var user = {
        username: "AdamBomb",
        password: "k@b00m!",
        name: "Adam Mark"
    };

    Kinvey.User.create(user,
        success: function(user) {
            console.log(user);
        },
        error: function(err) {
            console.log(err);
        }
    });

Together, App Cloud and Kinvey are a one-two punch for making high-performing,
cross-platform apps backed by powerful content and data services. To make it
easy for developers to get started with both platforms, App Cloud and Kinvey
collaborated on a [simple demo app][2] that shows how to create users and
store user data in the cloud.

Want to dive deeper? Check out the [Kinvey JavaScript Developer's Guide][3]
and the [Quick Start to App Cloud][4].

[1]: http://www.kinvey.com
[2]: http://docs.kinvey.com/js-app-cloud-tutorial.html
[3]: http://docs.kinvey.com/js-developers-guide.html
[4]: http://support.brightcove.com/en/docs/tutorial-creating-simple-app
[5]: http://appcloud.brightcove.com