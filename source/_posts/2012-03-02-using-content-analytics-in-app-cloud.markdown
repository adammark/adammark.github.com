---
layout: post
title: "Using content analytics in App Cloud"
date: 2012-03-02 17:19
comments: true
categories: [App Cloud, JavaScript]
---

The latest version of the App Cloud SDK (1.7.4) introduces content-level
analytics for tracking custom events in your template. It's a snap to use,
with just two methods:

    bc.metrics.startContentSession(contentURI, name)

The above method initiates a content session—for example, when a user begins
reading a news article. The first argument, `contentURI`, should be a unique
ID or URI. The second argument, `name,` should be a human-readable description
(e.g. an article title) for display in App Cloud Studio.

    bc.metrics.endContentSession(contentURI)

The above method ends the content session for the given `contentURI`. In the
case of tracking article views, you might invoke this method when the user
clicks "Back."

See the [App Cloud docs][1] for a complete rundown.

Two important notes: First, content-level analytics work only in production
mode, meaning you won't see data appear in App Cloud Studio until you publish
and deploy an app. Use `console.log()` to test your code during development.
Second, it's your responsibility to pause and unpause content sessions when
the user exits and reenters a view. You can do this by listening for
"viewblur" and "viewfocus" events.

Content-level analytics appear in the "Analytics" section of App Cloud Studio:

![Screen shot](/images/blog/app-cloud-content-analytics.png)

[1]: http://support.brightcove.com/en/docs/content-level-analytics