---
layout: post
title: "Three ways to use text blocks in App Cloud"
date: 2012-05-09 11:17
comments: true
categories: [App Cloud]
---

With [App Cloud][1] text blocks, you can store arbitrary blocks of text in the
cloud and retrieve them for any purpose you desire. Now you can bypass your
CMS (and your IT department!) when you need to manage certain types of
lightweight data in your apps.

To create a text block, go to the Content section of App Cloud Studio, then
click "New Content Source", then click "Text Content":

![Screen shot](/images/blog/app-cloud-text-new.png)

Then enter a name and some text. That's it! Whenever you want to change the
text, just click "Edit" and App Cloud will save a new version. (You can revert
to an old version at any time.)

At the code layer, you can request a text block with `bc.core.getData()`, just
like a content feed:

    bc.core.getData("my-text-block", function (data) {
        var myText = data.text;
        // do stuff
    });

Here are three ways to use text blocks inside your app:

## 1. HTML text

Use a text block as a flexible messaging area:

![Screen shot](/images/blog/app-cloud-text-html.png)

Then insert the text into DOM using jQuery or the method of your choice:

    bc.core.getData("welcome-message", function (data) {
        $("#welcome-message").html(data.text);
    });

## 2. JSON text

Use a text block to store structured data in JSON format:

![Screen shot](/images/blog/app-cloud-text-json.png)

When you load the text, make sure to parse it using JSON.parse():

    bc.core.getData("produce", function (data) {
        var produce = JSON.parse(data.text);
        ...
    });
 
## 3. CSV text

Store a table of information as CSV:

![Screen shot](/images/blog/app-cloud-text-csv.png)

After you load the data, split the lines, then split each line on the comma
characters:

    bc.core.getData("directory", function (data) {
        var people = [];
        var rows = data.text.trim().split("\n");

        for (var i in rows) {
            var row = rows[i].split(",");

            people.push({
                "firstName": row[0],
                "lastName": row[1],
                "phone": row[2],
                "title": row[3],
                "email": row[4]
            });
        }
    });

These are just a few ways to use text blocks. As you can see, you can save any
kind of text format you want—it's flexible by design!

[1]: http://appcloud.brightcove.com
