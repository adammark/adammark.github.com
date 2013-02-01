---
layout: post
title: "Understanding tap events in App Cloud"
date: 2012-01-26 16:23
comments: true
categories: [App Cloud]
---

Remember doing stuff like this?

    <div id="hello" onclick="alert('hello!')">Hello</div>

Or this?

    document.getElementById("hello").onclick = function (evt) {
        alert("hello!");
    });

Or this?

    document.getElementById("hello").addEventListener("click", function (evt) {
        alert("hello!");
    });

Or this, with jQuery?

    $("#hello").click(function () {
        alert("hello!");
    });

All four techniques accomplish the same goal. But on phones and tablets,
there's no such thing as a "click." In fact, there's no such thing as a "tap."
In [App Cloud][1], a tap event is a custom jQuery event that monitors touch
events (touchstart, touchmove, touchend) to determine when a user is actually
performing a tap. Here's how to capture it:

    $("#hello").bind("tap", function (evt) {
        alert('hello!');
    });

Above, we're listening for a custom tap on the element with the ID "hello." If
you log the `evt` object to the console, you'll see all kinds of juicy info.

Since jQuery works on collections of elements, it's very easy to listen for a
tap event on many things at once. For example, say you've got a list of
stooges:

    <ul id="stooges">
        <li id="larry">Larry Fine</li>
        <li id="curly">Curly Howard</li>
        <li id="moe">Moe Howard</li>
    </ul>

You can bind a tap event to every item in the list:

    $("#stooges li").bind("tap", function (evt) {
        alert(this.id);
    });

Inside the callback function, `this` refers to the DOM element that triggered
the event (because the function is bound to that element). So clicking on
"Larry Fine" would alert "larry". In addition to storing information in the ID
attribute, you can hang all kinds of data on an element with HTML5 
[data attributes][2]. For example:

    <ul id="foods">
        <li id="apple" data-food-type="fruit">Apple</li>
        <li id="banana" data-food-type="fruit">Banana</li>
        <li id="cucumber" data-food-type="veggie">Cucumber</li>
    </ul>

Then you can inspect this data as needed.

Finally, it's important to note that the [bind][3] function works only on
elements that already exist in the DOM. Since you'll be generating content
dynamically, you can use the live() function, which attaches event handlers to
the matched elements now or in the future. (In jQuery 1.7, the recommended
technique is to use [on][4].)

[1]: http://appcloud.brightcove.com
[2]: http://html5doctor.com/html5-custom-data-attributes/
[3]: http://api.jquery.com/bind/
[4]: http://api.jquery.com/on/