---
layout: post
title: "App Cloud vs. PhoneGap: Which hybrid-native platform is right for you?"
date: 2012-11-16 12:24
comments: true
categories: [App Cloud]
---

When I talk to developers about App Cloud, they often ask, “How is App Cloud
different from PhoneGap?” Without missing a beat, I give my stock answer:
“PhoneGap is great, but App Cloud gives you so much more.” The matter of
_more_ has always nagged at me—_more is not necessarily better_—so I decided
to do an apples-to-apples comparison from a Web developer’s perspective. I
built the same app twice, first with PhoneGap, then with App Cloud, and graded
each system on the strength of its platform capabilities, development model,
and service offerings.

_Spoiler alert: Both App Cloud and PhoneGap are winners! Skip to the end to see
my conclusions._

## First impressions

**PhoneGap:**  I located and downloaded the latest version of the 
[PhoneGap SDK][1] in about 15 seconds without any fumbling. This made a great 
first impression. And I noticed PhoneGap offers a public archive and full
documentation of its old SDKs, which gave me peace of mind as a developer.
Finally, I found [phonegap.com][31] to be neatly organized, with clear 
pathways to documentation, community support, and case studies.

![](/images/blog/app-cloud-phonegap-phonegap-download.png)

**App Cloud:**  I [registered for a free account][2] before downloading the
SDK. (If you’re impatient like me, you’ll find the registration step annoying.
But it’s necessary if you want to use cloud services like cloud compilation,
push notifications, and analytics.) After registering, I landed in App Cloud
Studio, where I found links to the SDK, the [Workshop][3] app, video tutorials
and community support. I downloaded the SDK and the Workshop app.

![](/images/blog/app-cloud-phonegap-studio-download.png)

## Getting started

**PhoneGap:**  I unzipped the SDK, cracked open the getting started guides,
and followed the instructions for setting up my development environments on
iOS and Android. What looked simple on paper turned out to be insanely
complicated.

[Getting started on iOS][4] required downloading and installing XCode. But to
download XCode, I had to upgrade my operating system to version 10.7 from
version 10.6.8. This took four hours.

[Getting started on Android][5] was even more of an exercise in patience. I
downloaded [Eclipse][6], then the [Android SDK][7], then the 
[Android Developer Tools plugin][8]. At each pass I was presented a dizzying 
array of options. For example, there were _12 versions_ of Eclipse and 
_11 versions_ of the Android SDK:

![](/images/blog/app-cloud-phonegap-android-sdk.png)

Whew! All told, getting started with PhoneGap took nearly a whole day, and I
had yet to write a single line of code.

**App Cloud:** [Getting started with App Cloud][9] was a breeze by comparison.
First I downloaded the [Workshop][3] app onto my iPhone and Android phone.
Then I unzipped the SDK, double-clicked the [Node.js][32] installer, ran the
startup script, and opened the App Cloud development server in my browser. In
about ten minutes, I was ready to start coding.

![](/images/blog/app-cloud-phonegap-node-console.png)

## Hello World!

**PhoneGap:** I opened XCode and followed PhoneGap’s “Hello World”
instructions for creating a new Cordova iOS project from a shell script. This
appeared to work until I tried running the project in the iPhone simulator:

![](/images/blog/app-cloud-phonegap-xcode-error.png)

As it turned out, the local copy of the [getting started guide][10] was out of
date and omitted a key step: installing the Cordova library. I deleted the
project, installed the Cordova library, and ran the script again. Then I
tweaked index.html and opened the app in the simulator:

![](/images/blog/app-cloud-phonegap-phonegap-hello.png)

Nice! Getting the app onto my iPhone was a bit trickier. I had to register my
device in the [iOS Provisioning Portal][11], then create a provisioning
profile, then create a development certificate, then install the certificate.
While these steps are necessary to create an iOS app in any framework, it was
cumbersome to go through these motions just to run my “Hello World” app.

As for Android, it once again threw me for a loop. I simply couldn’t get my
“Hello World” app to run in the Android Emulator despite all my attempts to
create and launch an Android Virtual Device in Eclipse. After a frustrating
couple hours—even stackoverflow was no help—I managed to create a device image
via the Android SDK Manager, then launch the emulator:

![](/images/blog/app-cloud-phonegap-android-emulator.png)

**App Cloud:** I ran the provided Node.js script to create a starter app
inside App Cloud’s development server. Then I popped open Chrome and navigated
to the app:

![](/images/blog/app-cloud-phonegap-node-scaffold.png)

I made a few changes to a CSS file and refreshed the web browser—a quick win.
Then I opened the Workshop app on my iPhone and scanned the QR code that
appeared in the web browser. In three seconds, the app loaded on my phone. I
made some more changes to the CSS and pulled down the “Refresh” tab in the
Workshop. The changes appeared. Then I did the same thing on my Galaxy Nexus.

![](/images/blog/app-cloud-phonegap-workshops.png)

_By now I’ve gone through this process a thousand times, yet I’m always
floored by it._ In just a few minutes, I was previewing an app on both iOS and
Android, making changes, and seeing the changes take effect immediately. And I
did it without XCode, without the Android Developer Tools, and without any
specific knowledge of native app development.

## Structuring the app

**PhoneGap:** I wanted my sample app, a simple news reader, to have two
distinct views, one for displaying the latest news and one for displaying my
saved articles. I assumed I could use two HTML pages to create the backing for
these views, but I was surprised to learn that I had to build my entire
PhoneGap app within the context of a single HTML page. I imagined my code
would get pretty messy without using a JavaScript MVC framework to manage it,
and I worried about the performance implications of doing too many things
inside one page.

I was also disappointed by the lack of support for native navigation across
iOS and Android, so I had to roll my own navigation in HTML. Not wanting to
use an iOS-style tab bar on Android or an Android-style action bar on iOS, I
settled on a generic design that would accommodate both platforms.

Finally, I found no built-in functions for handling basic tasks like scrolling
and pagination. After exploring a few different UI libraries, I decided to
install [jQuery Mobile][12], a popular tool for building mobile web sites.

**App Cloud:** Unlike PhoneGap, App Cloud apps are backed by multiple HTML
files, each corresponding to an independent view in the UI. A typical
content-driven app might have four or five views, and the developer can choose
whether or not to display native navigation to help the user navigate from
view to view. In this sense, the UI is truly “hybrid.” On iOS, users see the
familiar tab bar and “More ...” menu; on Android, users see an action bar.

As I discovered early on, spreading code and functionality across multiple
views is a good thing for a few reasons. First, the native container can
unload individual views if it needs to free up memory (instead of crashing).
Second, developers can neatly organize their code by view (each HTML page has
its own DOM, its own CSS, and its own JavaScript). Finally, because the app is
broken into multiple views, the code itself is more portable.

![](/images/blog/app-cloud-phonegap-structure.png)

App Cloud has a thin UI layer, but it does 90% of what I need: “tap” events,
smooth scrolling, and page transitions inside a single view. I like having
these basic functions available out of the box. As with PhoneGap, App Cloud
lets you drop in third-party JavaScript libraries. (I’ve used many, including
[Moment.js][13] for date formatting and [Hammer.js][14] for gesture support.)

Another nice feature: App Cloud loads HTML “templates” from plain text files
on the device’s file system and populates them in the `bc.templates` object.
This makes it easy to separate control logic from presentation logic using
Markup.js (included in the App Cloud SDK) or a templating framework of your
choosing.

## Making the app

**PhoneGap:** Even though I was able to use my [favorite text editor][15] and
stage the app on a local web server (Apache), I still had to run XCode and
Eclipse in order to build and preview the app on my iPhone and Nexus. Every
few minutes I went through the same motions: _1. Switch contexts from my text
editor to Xcode, then to Eclipse. 2. Run the app in the iPhone simulator, then
in the Android emulator. 3. Deploy to each device._ This got tiresome. (I
looked at [PhoneGap Build][16] as a potential time saver, but it didn’t strike
me as a convenient development tool. It’s a build tool, as the name implies. I
also looked at [Hydration][17] but got scared away by the docs. What’s a 
“non-Hydrated binary equivalent?”)

At this point it occurred to me that I was dealing with two different code
bases to make two different apps, one for iOS and one for Android. A fellow
engineer suggested I create a symbolic link between the www directories in
each project, which seemed kludgy to me.

**App Cloud:** I staged my app in App Cloud’s local development server
(running on Node.js) and tested much of it in Chrome. When it came to testing
the app on my iPhone and Nexus, I simply loaded it up in the Workshop app.

![](/images/blog/app-cloud-phonegap-reload.png)

The Workshop app extends the development model that all web developers have
come to know: _Code, refresh, repeat._ The ability to test an app
incrementally—without long delays and without having to reboot the app—saves a
tremendous amount of time and frustration.

Finally, unlike PhoneGap, I was working with a single code base of HTML, CSS,
and JavaScript files, even though I was building for iOS and Android at the
same time. There was simply less code to move around.

## Working with content

**PhoneGap:** I pulled an RSS feed directly from my web site using jQuery’s
[get()][18] method. Then I converted it to JavaScript object with the help of
an [XML to JSON plugin][19]. To cache content on the device, I used
[Local Storage][20] methods.

**App Cloud:** As with PhoneGap, I used `$.get()` to pull down the RSS. When
it came to storing data on the device, I used [bc.core.cache()][33], which
uses a Least Recently Used algorithm to clear data if the cache ever fills up.
App Cloud’s caching function also handles serialization and deserialization of
objects.

Taking it a step further, I decided to run my data through an App Cloud
content feed, then load it using the SDK method [bc.core.getData()][21]. This
service has multiple benefits: First, it lightens the load on the origin
server (in my case, a small Wordpress site). The App Cloud server periodically
fetches new data, caches it, and makes it highly available to thousands of
devices. Second, App Cloud reduces the size of the payload by eliminating
unnecessary data fields. Third, App Cloud converts the data from XML to JSON
on the server side, flattens it, compresses it, and provides a convenient
interface for accessing it.

![](/images/blog/app-cloud-phonegap-feeds.png)

## Working with the device

**PhoneGap:** While I didn’t really take advantage of native device
capabilities, I noticed that PhoneGap’s device API is more mature than App
Cloud’s. For example, PhoneGap supports access to the [contacts database][22]
and [compass][23]. It also has a nice interface for determining the device’s
[connection type][24]. And the API itself is very well organized.

**App Cloud:** While App Cloud offered less in the way of device capabilities,
there were some built-in features that I found to be invaluable. First, it’s
often necessary to display external web content without forcing the user to
leave the app. For this reason, the App Cloud SDK makes it extremely easy to
open native modal windows. (PhoneGap has some plugins for this, but they
require extra configuration.) Second, many types of content apps require
multiple, distinct views. By default, App Cloud supports multiple views backed
by native navigation controls. Developers can hide the navigation bar outright
or toggle it via [bc.device.enterFullScreen()][25] and
[bc.device.exitFullScreen()][26].

_Note: App Cloud will soon release its own plugin development kit that allows
developers to create custom native functionality on top of the App Cloud SDK._

## Running the app

**PhoneGap:** From a distance, it was hard to distinguish between PhoneGap and
App Cloud. But there were a couple issues with PhoneGap. First, I was unhappy
with the smooth scrolling (or lack thereof) in jQuery Mobile, my chosen UI
layer. I considered switching to [Kendo UI Mobile][27], but I didn’t want to pay
$199 for it. I also looked at [Sencha Touch][28], but it was too bulky (a 55MB
download). I settled on iScroll. Problem solved. Second, the part of my UI
that displayed multiple images (at 150KB each) was noticeably slower to load.

**App Cloud:** I cheated here and used App Cloud’s [image transcoding API][29],
even though it’s not part of the free edition (App Cloud Core). I cropped and 
scaled each thumbnail image on the fly, shaving nearly 1MB off the total 
payload and speeding up the rendering of the UI. Sure, I could have cut
up these images by hand, but that’s simply not practical to do when delivering
dynamic images to multiple platforms across many types of devices.

I also saved a few cycles by loading my data through an App Cloud content
feed. Not only was the payload smaller, I didn’t need to convert it from XML
to JSON on the client.

App Cloud’s smooth scrolling was also faster than iScroll when handling
complex content.

One final note on performance: Both apps ran faster on iOS than on Android.

## Building the app

**PhoneGap:** Since I had already done the hard work of setting up XCode and
the Android Developer Tools, building the app for production was relatively
straightforward. I just repeated what I had already done a dozen times during
development (although I added my own icons and loading images).

**App Cloud:** I zipped up the directory containing my static assets—HTML,
CSS, JS, etc.—and uploaded it to App Cloud Studio. Then I clicked “Publish
App” and was asked to enter tons of provisioning information for iOS and
Android. Although tedious, this process was certainly easier than having to
build the apps myself, and at the end I was able to download an IPA file for
iOS and an APK file for Android.

![](/images/blog/app-cloud-phonegap-studio-download.png)

## And the winner is ...

I think PhoneGap and App Cloud are both winners, but in different categories.
PhoneGap wins for having a more robust device API, great documentation and
examples, and a large ecosystem of plugins. (As I mentioned above, App Cloud
is about to release its own plugin framework, and it will support many
PhoneGap plugins.) App Cloud wins for its elegant development model—_the
Workshop app is simply unmatched_—and for its array of cloud services.

The biggest distinction is this: While PhoneGap is a development platform, App
Cloud is a development platform and an operational platform at the same time.
In my simple demo app, I took advantage of two App Cloud services: image
transcoding and content feed optimization. I also compiled my iOS and Android
apps in the cloud from a single code base. In a more complex app, I would use
App Cloud’s [push notification API][30], real-time analytics, and remote
configuration capabilities. Sure, these things are possible with PhoneGap, but
not without cobbling together lots of moving parts from many different
vendors.

I encourage web developers who are exploring hybrid-native solutions to
evaluable both platforms as I have. You might find PhoneGap to be exactly what
you’re looking for: a cross-platform development kit. But if you need more in
the way of services (image transcoding, content optimization, push
notifications, etc.) and less in the way of heavy toolchains (XCode and
Eclipse), take App Cloud for a spin.

Both App Cloud and PhoneGap have a lot to offer. I hope they continue to push
each other—and web developers—forward.

[1]: http://phonegap.com/download
[2]: https://register.brightcove.com/en/app-cloud
[3]: http://bit.ly/iworkshop
[4]: http://docs.phonegap.com/en/2.0.0/guide_getting-started_ios_index.md.html
[5]: http://docs.phonegap.com/en/2.0.0/guide_getting-started_android_index.md.html
[6]: http://www.eclipse.org/downloads/
[7]: http://developer.android.com/sdk/installing/index.html
[8]: http://developer.android.com/tools/sdk/eclipse-adt.html#installing
[9]: http://docs.brightcove.com/en/app-cloud-api/quick-start-app-cloud.html
[10]: http://docs.phonegap.com/en/2.0.0/guide_getting-started_ios_index.md.html
[11]: https://developer.apple.com/ios/
[12]: http://jquerymobile.com/
[13]: http://momentjs.com/
[14]: http://eightmedia.github.com/hammer.js/
[15]: http://www.sublimetext.com/2
[16]: https://build.phonegap.com/
[17]: https://build.phonegap.com/docs/hydration
[18]: http://api.jquery.com/jQuery.get/
[19]: http://www.fyneworks.com/jquery/xml-to-json/
[20]: http://diveintohtml5.info/storage.html
[21]: http://docs.brightcove.com/en/app-cloud-api/core/symbols/bc.core.html#.getData
[22]: http://docs.phonegap.com/en/2.0.0/cordova_contacts_contacts.md.html#Contacts
[23]: http://docs.phonegap.com/en/2.0.0/cordova_compass_compass.md.html#Compass
[24]: http://docs.phonegap.com/en/2.0.0/cordova_connection_connection.md.html#Connection
[25]: http://docs.brightcove.com/en/app-cloud-api/core/symbols/bc.device.html#.enterFullScreen
[26]: http://docs.brightcove.com/en/app-cloud-api/core/symbols/bc.device.html#.exitFullScreen
[27]: http://www.kendoui.com/mobile.aspx
[28]: http://www.sencha.com/products/touch/
[29]: http://support.brightcove.com/en/docs/transcoding-images
[30]: http://blog.brightcove.com/en/2012/04/using-cross-platform-push-notifications-app-cloud
[31]: http://phonegap.com/
[32]: http://nodejs.org/
[33]: http://docs.brightcove.com/en/app-cloud-api/core/symbols/bc.core.html#.cache