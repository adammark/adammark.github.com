---
layout: post
title: "Bug off! App Cloud introduces on-device debugging"
date: 2012-07-12 10:35
comments: true
categories: [App Cloud]
---

Bugs are a way of life in both the physical and virtual worlds. In the
physical world, we can “debug” with fly swatters and bug spray. In the virtual
world, debugging is a bit more sophisticated, as software bugs can be
invisible and unpredictable.

It's doubly hard to identify and kill bugs running on a mobile device—unless
you have the right tools. [App Cloud][3] developers already have the
[Workshop][1] app for previewing and interacting with their work in real time.
Now they can take advantage of on-device debugging—also called _remote
debugging_—to remotely inspect and tune their code. Here's how it works:

First, go to the "On-Device Debugging" page in App Cloud Studio. Then open an
app in the Workshop and give the device a good shake. When the camera
launches, scan the QR code that appears in the Studio:

![Screen shot](/images/blog/app-cloud-debug-scan.png)

Once a connection is established, you'll see a debug panel in the Studio that
looks like the Chrome Developer Tools. From here, you can remotely inspect and
modify the DOM, issue JavaScript commands, and more:

![Screen shot](/images/blog/app-cloud-debug-console.png)

As a test, click the "Console" tab and type `bc.device.alert("Whoa!")`. You'll
see an alert pop up on the device!

App Cloud's on-device debugging is based on the open source [Weinre][2]
project. It's a great tool for developers who want to build rock-solid apps
quickly and easily.

[1]: http://bit.ly/iworkshop
[2]: http://phonegap.github.com/weinre/
[3]: http://appcloud.brightcove.com
