---
layout: post
title: "Inside the App Cloud Workshop: Understanding your apps in development mode"
date: 2012-08-03 15:55
comments: true
categories: [App Cloud]
---

The [App Cloud][8] Workshop app for [iOS][1] and [Android][2] is an amazing
tool for app developers. It lets you preview your apps in the palm of your
hand without the need for complex toolchains like XCode or the Android
Developer Tools, and it mimics the web development workflow: _Code, Refresh,
Repeat_.

![App Cloud Workshop](/images/blog/app-cloud-workshop.jpg)

But there are some subtle differences between how an App Cloud app behaves in
_development mode_ and how it behaves in _production mode_ as a compiled
binary. Here’s what you should keep in mind:

* Your app will load a bit more slowly in development mode because all of its
assets—HTML files, scripts, stylesheets, images, etc.—are fetched from an
external server. In a compiled app, most or all of these assets will be baked
into the binary package and loaded from disk.

* In development mode, your app will open without a launch icon or splash
screen. These assets are added during the [publishing process][3]. When a user
opens your published app, they’ll see the launch screen for a few seconds as
the app loads.

* You might see a blank white screen in the Workshop as you load and refresh
each View. In a compiled app, you might only see this happen if a View is
“torn down” by the app container in order to reclaim memory, or if your app
has Views that live deep inside the “More ...” menu.

* In the Workshop, a developer can refresh individual Views and even restart an
app when it behaves poorly or strangely, but these options aren’t available to
users in a published app. (Developers should “stress test” their finished apps
for extended periods of time in order to identify issues that might only
surface after heavy use.)

* Some device functions behave differently in the Workshop. For example, when
downloading a file with the [File Download API][4], the downloaded file is
inaccessible in the Workshop. This particular quirk and others are explained
in the App Cloud [API docs][5].

* A few App Cloud services don’t work in development mode, including push
notifications and analytics.

The only way to truly test the behavior of your finished app is to publish it
and install it on your device before deploying it to the app stores. On iOS,
you can create a development certificate or [_ad hoc_][6] certificate for this
purpose. On Android, you can [side-load][7] your app onto a phone or tablet.

When used properly and in tandem with rigorous testing practices, the Workshop
is an invaluable part of the App Cloud experience. Pretty soon you’ll wonder
how you ever got by without it!

[1]: http://bit.ly/iworkshop
[2]: http://bit.ly/aworkshop
[3]: http://support.brightcove.com/en/docs/publishing-app
[4]: http://blog.brightcove.com/en/2012/07/get-download-app-clouds-file-download-api
[5]: http://docs.brightcove.com/en/app-cloud-api/core/index.html
[6]: http://stackoverflow.com/questions/4955605/what-is-an-adhoc-certificate
[7]: http://www.techrepublic.com/blog/smartphones/how-to-side-load-apps-on-your-android-device/3114
[8]: http://appcloud.brightcove.com