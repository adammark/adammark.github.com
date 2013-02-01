---
layout: post
title: "Digging deeper into App Cloud data feeds"
date: 2012-07-30 10:39
comments: true
categories: [App Cloud, JavaScript]
---

Smart Content Sources are a quick and easy way to load data into your 
[App Cloud][1] apps. Let's take a look at what happens under the hood when 
you load a content source with `bc.core.getData()`:

![Screen shot](/images/blog/app-cloud-feeds-new.png)

First, no matter what kind of data you're loading from App Cloud—a Video Cloud
playlist, a content feed, or a text block—you can call it the same way in your
code:

    bc.core.getData("1234567890", handleData, handleError);

Above, "1234567890" is the ID provided by App Cloud Studio. You can also
declare the feed in your manifest file and call it by name:

    bc.core.getData("blog", handleData, handleError);

The function `getData()` is asynchronous. When it runs successfully, the SDK
calls `handleData`; otherwise, it calls `handleError`. The success handler
takes a single argument:

    function handleData(data) {
        console.log(data);
    }

If you log the data to the console, as shown above, you might see an object
like this one, which comes from a Video Cloud playlist:

![Screen shot](/images/blog/app-cloud-feeds-inspect.png)

So what's happening under the hood?

The App Cloud SDK injects a `<script>` tag into the document and sets the `src`
attribute to the URL of a content feed:

    <script src="http://read.appcloud.brightcove.com/content/50019dfcec8e60277d00fdb8/
    fetch?callback=jQuery17207518197379540652_1343651580663&_=1343651580663"></script>

This process has the curious name [JSON-P][3], or "JSON with padding." Notice
the URL contains the name of a callback function to execute when the script is
loaded.

When the script is loaded, it executes a function that wraps (or "pads") a
JSON object. Here's what it looks like inside the Network panel of the Chrome
Developer Tools:

![Screen shot](/images/blog/app-cloud-feeds-response.png)

This function, in turn, hands off the data to the callback function specified
in `bc.core.getData()`.

As you can see, it's easy to inspect your data using the Chrome Developer
Tools. And if you want to dig even deeper, consider using an HTTP monitor like
[Charles][2].

Finally, keep in mind that `bc.core.getData()` is just one way to load data
into your app. You can also use the device functions `fetchContentsOfURL()`,
`postDataToURL()`, and `requestDownload()`.

[1]: http://appcloud.brightcove.com
[2]: http://www.charlesproxy.com/
[3]: http://en.wikipedia.org/wiki/JSONP
