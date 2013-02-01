---
layout: post
title: "Using Dropbox to host your App Cloud app in development mode"
date: 2012-04-02 17:07
comments: true
categories: [App Cloud]
---

If you can't create a local web server for any reason—too lazy, too many
network restrictions, what's a web server?—you can use a public [Dropbox][1]
folder instead.

Just drop your template into the "Public" folder inside your Dropbox
directory. Then right-click on your manifest file (manifest.json) and select
_Dropbox > Copy Public Link_. You should get a URL like this:

    http://dl.dropbox.com/u/12345678/mytemplate/manifest.json

Enter this URL in the [Workshop app][2] and you're off to the races! You can also
view your HTML pages in Chrome and debug them with the Developer Tools.

_Warning! Your files will be accessible to anyone who knows the URL, so share wisely._

[1]: http://www.dropbox.com/
[2]: http://bit.ly/iworkshop