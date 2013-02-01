---
layout: post
title: "App Cloud content feeds: Getting to green"
date: 2012-01-31 17:46
comments: true
categories: [App Cloud]
---

I just smashed my personal content feed optimization record in [App Cloud][1].
The [original feed][2], a YouTube playlist, clocked in at 176KB. _Whoa._

So how’d I do it? First, I limited the number of entries to 20 (the original
feed had 25). Then I eliminated all the fields I didn't need, leaving only
9 or 10.

![Screen shot](/images/blog/app-cloud-optimization.png)

The result: 20KB. _A nearly 90% reduction!_ As soon as I tamed this bad boy,
my app sped up noticeably. Not only does the payload come down faster, the app
can process it faster.

[1]: http://appcloud.brightcove.com
[2]: https://gdata.youtube.com/feeds/api/playlists/92E2F27744E3DC5F?v=2