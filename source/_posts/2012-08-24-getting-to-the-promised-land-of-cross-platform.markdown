---
layout: post
title: "Getting to the promised land of cross-platform, device-independent displays"
date: 2012-08-24 15:33
comments: true
categories: [App Cloud, CSS, Design]
---

I've been leaning heavily on [CSS Media Queries][2] and [Flexbox][3] to build
[App Cloud][7] apps that adapt to both portrait and landscape modes. For
example, I made a video playlist that flows from top to bottom in portrait
mode and left to right in landscape mode:

![Portrait and landscape orientations](/images/blog/app-cloud-orientation.jpg)

I also use CSS to build “universal” apps that adapt intelligently to different
form factors. The properties `min-device-width` and `max-device-width` can
help detect whether an app is running on something the size of a phone or
something the size of a tablet. Smashing Magazine has a [good tutorial][1] on
this subject.

But CSS alone can't get me to the promised land of cross-platform, 
device-independent displays. Here's where it comes up short:

* **CSS can't change the behavior of an app.** It can only affect presentation
characteristics. Except for toggling the visiblity of certain page elements or
adjusting their metrics, it's nearly impossible to apply device-specific or
orientation-based functionality without the help of JavaScript.

* **CSS can't resize images.** Yeah, you heard me. CSS can scale down an
image, but it can't resize an image. A 250KB image is still 250KB whether you
display it at 100% or 50% of its intrinsic size. To properly scale images for
all kinds of devices, you'll need the help of a transcoding service.

Getting to the promised land—we're talking about apps that adapt to portrait
and landscape modes and work across a variety of devices and perform really
well—is easy with App Cloud. Here's how.

## Responding to orientation changes

If you know the current orientation—and if you know when it changes—you can
make intelligent decisions about the user experience. For example, you might
want to load some extra data or transform the UI entirely when the user
switches into landscape mode:

    // get the current orientation ("landscape" or "portrait")
    var orientation = bc.context.viewOrientation;

    // listen for an orientation change
    $(bc).on("vieworientationchange", function (evt, result) {
        orientation = result.orientation;

        if (result.orientation === "landscape") {
            // do something!
        }
        else {
            // do something else!
        }
    });

## Distinguishing between phones and tablets

If you know whether your app is running on a phone or tablet, you can deliver
specific functionality to each form factor from a single codebase. For
example, here's a factory method that instantiates one type of BlogView if
running on a phone, another if running on a tablet:

    BlogView.factory = function () {
        return getDeviceType() === "phone" ? new PhoneBlogView() : new TabletBlogView();
    };

There are a few ways to determine the device type. A simple method is to look
at the width and height of the window, multiply them together, and evaluate
the result:

    function getDeviceType() {
        return innerWidth * innerHeight <= 320 * 480 ? "phone" : "tablet";
    }

Here's a similar technique from [HTML5rocks.com][4]:

    function getDeviceType() {
        return window.matchMedia("(max-width: 650px)").matches ? "phone" : "tablet";
    }

These methods are great if your definition of a phone is somewhat fast and
loose (some Android phones are as big as tablets). Instead, consider
categorizing your target devices as "big" and "small":

    function getDeviceType() {
        return window.matchMedia("(max-width: 650px)").matches ? "small" : "big";
    }

## Distinguishing between operating systems

Sometimes it's necessary to know which operating system you're running on. App
Cloud makes this easy:

    var os = bc.context.os;

    if (os === "ios") {
        // do something
    } else if (os === "android") {
        // do something else
    }

In the above example, "doing something" might mean loading different
stylesheets or disabling a certain feature that isn't available on Android.

## Resizing images

The pièce de résistance of responsive design is being able to resize and crop
images on the fly based on runtime conditions such as screen size and pixel
density. You can do this with App Cloud's [image transcoding API][5].

![Before and after images](/images/blog/app-cloud-transcode-before-after.jpg)

It's easy to use JavaScript to compose service URLs based on screen metrics or
other layout constraints. Here's a simple example:

    function transcode(src, width, height) {
        return "http://transcode.appcloud.brightcove.com?image=" + src +
            "&width=" + width + "&height=" + height;
    }

If you want to support retina displays, just double the width and height if
`window.devicePixelRatio` equals 2:

    function transcode(src, width, height) {
        if (window.devicePixelRatio === 2) {
            width *= 2;
            height *= 2;
        }

        return "http://transcode.appcloud.brightcove.com?image=" + src +
            "&width=" + width + "&height=" + height;
    }

Retina images are typically four times as big as normal images (double the
width times double the height), so consider using a multiplier between 1 and 2
to lighten the load a bit while still improving quality.

You can also crop images with the image transcoding API rather than rely on
CSS tricks. Remember, every bit counts in a mobile app. Load only what you
need when you need it.

## Learn more

You can see all of these techniques at work in the [App Cloud Demos][6]
repo on GitHub. The promised land is closer than you think!

[1]: http://mobile.smashingmagazine.com/2010/07/19/how-to-use-css3-media-queries-to-create-a-mobile-version-of-your-website/
[2]: http://www.w3.org/TR/css3-mediaqueries/
[3]: http://www.html5rocks.com/en/tutorials/flexbox/quick/
[4]: http://www.html5rocks.com/en/mobile/cross-device/
[5]: http://support.brightcove.com/en/docs/transcoding-images
[6]: https://github.com/BrightcoveOS/App-Cloud-Demos
[7]: http://appcloud.brightcove.com