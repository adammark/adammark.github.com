---
layout: post
title: "Get the download on App Cloud's File Download API"
date: 2012-07-11 10:30
comments: true
categories: [App Cloud, JavaScript]
---

Your content-centric app is only as good as the network it's running on—until
now. With [App Cloud's][3] [File Download API][1], you can permanently store
all kinds of media assets on the device for offline use. Text feeds, images,
PDF documents, audio and video files, you name it. This presents lots of
possibilities for app developers:

* Your apps can degrade gracefully when the user's network goes in and out

* You can program your apps to front-load content so they work perfectly in
"airplane mode"

* You can allow users to create custom content experiences that work anywhere,
anytime

Of course, your app can do all of the above. Here's a quick look at the
methods and events in the File Download API:

### Methods

* `bc.device.requestDownload()`: Download a file from a remote URL

* `bc.device.removeDownload()`: Delete a previously downloaded file

* `bc.device.isDownloadAvailable()`: Determine if the device supports file downloading

* `bc.device.getDownloadInfo()`: Get information about previously downloaded files

As with other device methods, these are asynchronous—you must provide success
and error callbacks.

### Events

* `downloadprogress`: Dispatched on each progress event at the specified interval (e.g. 5%) (iOS only)

* `downloadcomplete`: Dispatched when a download finishes

* `downloaderror`: Dispatched on certain error conditions

The API is low-level by design, requiring you to use bc.core.cache() to store
associated metadata in most situations. I've written a `FileManager` object to
hide some of the implementation details of downloading, retrieving and
deleting files—check it out in the [App Cloud Demos][2] repo, then get
downloading!

[1]: http://support.brightcove.com/en/app-cloud/docs/downloading-files-using-app-cloud-api
[2]: http://opensource.brightcove.com/project/app-cloud-demos
[3]: http://appcloud.brightcove.com