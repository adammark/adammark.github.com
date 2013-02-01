---
layout: post
title: "The Pursuit of Appiness: Building native apps with App Cloud and HTML5"
date: 2011-12-05 16:41
comments: true
categories: [App Cloud]
---

As a web developer and designer for thirteen years, I've jockeyed from one hot
technology to another with relative ease. First Java, then PHP, then Ruby. I
rode the Flash train for a long time. I kept up with every major UI library,
from Prototype to jQuery, and kept pace with rapidly evolving web standards.

But like many web developers, I missed the boat on mobile. I had no experience
with low-level programming languages like C++ or Objective-C, nor did I have
time to learn them. And the thought of making _small_ apps with Java—a language
that always seemed big and bulky to me—was unappealing.

I looked at a number of products for cross-platform development, but every one
fell short of my expectations:

* App "factories" that wrap RSS feeds in prefab templates tend to produce low-
budget or cookie-cutter apps.

* Frameworks that convert JavaScript or ActionScript into native code require
complex toolchains to create and compile the apps.

* Frameworks that wrap web pages in native shells provide little or no back-end
infrastructure necessary to operate data-driven apps in production.

So when I learned about [App Cloud][1], a framework for creating native mobile
apps with HTML, CSS and JavaScript, I was skeptical. Would App Cloud be
different from the other products I tried? Would it live up to its many
promises? I set out to make a real app and learned the answer is a resounding
YES. Here's why:

## App Cloud speaks my language

App Cloud draws on all my skills as a web developer: HTML to structure
content, CSS to style it, and JavaScript to manipulate it. I don't have to
learn new languages to create rich, content-driven apps. After all, web
technologies have always excelled in this area. Compare the complexity of
[creating a table view in iOS][2] to the simplicity of creating a list of
things in HTML. (There is no comparison.)

![](/images/blog/app-cloud-appiness-html5.png)

Plus, I can use almost any JavaScript libraries I want on top of the App Cloud
SDK. After many years of web development, I came to App Cloud with a big bag
of tricks that I didn't want to throw away.

## It’s my way or the highway

When I write code, I alternate between using [Sublime Text][3] and vim. So
when I jumped into App Cloud, I was relieved to find that I could use my
trusty tools. And since App Cloud uses standard web technologies, I can use
[Chrome Developer Tools][4] to inspect and debug my code on the desktop.

While some other systems ride the coattails of XCode or Eclipse—a bulky and
maddeningly complex Java-based IDE—App Cloud gives me freedom of choice.

## The Workshop—it’s refreshing!

The App Cloud [Workshop app][5] for iOS and Android lets me test and
experience my apps as I develop them. I change some code, click "Refresh," and
see the results immediately. As a web developer, I rely on this kind of rapid
iteration. _Code, refresh, repeat._

![](/images/blog/app-cloud-appiness-workshop.jpg)

While much of my work can be tested in a desktop web browser, there's no
substitute for actually experiencing the app running on real devices. The
Workshop app makes this process a snap.

## There’s an API for that

App Cloud provides a ridiculously simple JavaScript bridge to native device
capabilities like the camera and photo library—things that aren't possible in
a regular mobile web site. Here's how to access the camera to scan a QR code:

    bc.device.getQRCode(successCallback, errorCallback);

That was easy! And it works across iOS and Android, tablet and phone. I don't
need to worry about the underlying characteristics of each platform or device
form factor. It just works.

## App Cloud Studio: Compile in style

I recently [installed the Android developer tools][6] to compile an app I made in
another framework, an exercise not unlike building an IKEA bookshelf. The
directions were incomprehensible, it took half a day, and the results were a
bit rickety.

With App Cloud Studio, my apps are compiled in the cloud with the touch of a
button (okay, a few buttons). In just a few minutes, the compiled apps are
ready for download, at which point I can submit them to the various app
stores. Absolutely no special tooling is required on my end.

![](/images/blog/app-cloud-appiness-download.jpg)

## Content optimization: Less is more

In content-driven apps—and especially in content-driven mobile apps—the
biggest bottleneck is the content itself. App Cloud speeds up my apps in a
couple important ways:

* App Cloud removes unnecessary and unwanted data from my content feeds. Then it
compresses them, caches them, and makes them highly available to thousands of
devices. My blog feed went from 39KB to 4KB after optimization and
compression, a 90% reduction!

* App Cloud resizes and caches images _on the fly_. The cumulative effects of
image transcoding cannot be overstated: one of my blog images was reduced from
125KB at 425px wide to 8KB at 200px wide, a 94% reduction! Multiply this by
the number of images in my blog, the number of users, and the number of
sessions per user. We're talking big, big savings.

![](/images/blog/app-cloud-appiness-transcode.jpg)

Studies have shown that [load time affects the bottom line][7]. With App
Cloud, it's one less thing I have to worry about.

## Set and forget? Not with App Cloud

Do you remember the Showtime Rotisserie Oven? You [_set it and forget it!_][8]
If only apps were this simple. Content-driven apps, like web sites, often
require configuration changes after being deployed. With App Cloud Studio, I
can change data, styles and other custom settings after an app has been
deployed and without recompiling and resubmitting the app to the various app
stores.

![](/images/blog/app-cloud-appiness-config.jpg)

This not only gives me a ton of flexibility as a developer, it empowers others
in the organization to help manage the apps I create.

What's more, the ability to change data, settings and styles in App Cloud
Studio means I can create _multiple apps from a single template_ without
writing any additional code. I didn't fully appreciate this power until I made
two very distinct apps from the same template:

![](/images/blog/app-cloud-appiness-template.jpg)

All I did was swap out data feeds and adjust a few settings. The design and
configuration options were entirely up to me.

## Sharing is caring

While App Cloud doesn't solve the problem of hovering art directors, it does
make it easier for colleagues to review my work in the comfort of their own
offices. For example, I can send screenshots directly from the Workshop app:

![](/images/blog/app-cloud-appiness-capture.jpg)

Or I can share an entire template with anyone who has the Workshop app just by
sending them a URL or QR code:

![](/images/blog/app-cloud-appiness-scan.jpg)

## 100% Cloud coverage

App Cloud is a one-stop shop for nearly everything I need to manage and
monetize my content apps in production, from native ad insertion to real-time
analytics. For example, in the Analytics section, I can see how my apps are
performing in the wild, from total installs to total usage time:

![](/images/blog/app-cloud-appiness-analytics.jpg)

And because App Cloud is service-oriented and all-inclusive, I get performance
enhancements and feature updates for free. I'm excited for what's to come:
push notifications, in-app purchases, Facebook integration, additional
platform support, and more.

If you're still reading, you're probably interested in trying App Cloud for
yourself. Just [register for a free account][9] and download the SDK from
App Cloud Studio.

Happy (er, "appy") developing!

[1]: http://appcloud.brightcove.com
[2]: http://developer.apple.com/library/ios/#documentation/userexperience/conceptual/TableView_iPhone/CreateConfigureTableView/CreateConfigureTableView.html
[3]: http://www.sublimetext.com/2
[4]: http://code.google.com/chrome/devtools/
[5]: http://bit.ly/iworkshop
[6]: http://developer.android.com/sdk/installing.html
[7]: http://blog.kissmetrics.com/loading-time/?wide=1
[8]: http://www.youtube.com/watch?v=O5s1jY1Nwl4&t=81
[9]: http://register.brightcove.com/app-cloud