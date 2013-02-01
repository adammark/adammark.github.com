---
layout: post
title: "More JavaScript tricks to impress your friends"
date: 2011-10-02 18:00
comments: true
categories: [JavaScript]
---

And now for another installment of cool but unreadable JavaScript techniques!

### Repeating a string

Use the Array constructor to repeat a string. For example, to create the
string “**********”:

    // old way
    var str = "";
    for (var i = 0; i < 10; i++) {
        str += "*";
    }

    // ninja way
    var str = Array(11).join("*");

In the ninja example above, an array with 11 empty values ("") is joined by
“*”. (Thanks to [JavaScript Garden][1].)

### Casting function arguments to an array

Sometimes you need to treat function arguments as an array:

    // old way
    function func(a, b, c) {
        var arr = [];
        for (var i in arguments) {
            arr.push(arguments[i]);
        }
    }

    // ninja way
    function func(a, b, c) {
        var arr = [].slice.call(arguments);
    }

Calling `Array.prototype.slice`, or `[].slice` on the arguments object returns
an array of arguments. Now you can pass it around or slice and dice it.

### Testing for even or odd

In my [tutorial on bitwise operations][2], I explained how to use a bitwise
AND to test if a number is even or odd:

    // old way
    if (i % 2 == 0) { … }

    // ninja way
    if (i & 1 == 0) { … }

In binary, an even number AND 1 is always 0 (even); an odd number AND 1 is
always 1 (odd).

### Testing minimum length of a list

Sometimes (or never) you need to know whether a list is at least a certain
length:

    var list = ["a", "b", "c"];

    // old way
    if (list.length >= 3) { … }

    // ninja way
    if (2 in list) { … }

Wait, what? Imagine the above array as an object literal:

    var list = {
        0: "a",
        1: "b",
        2: "c"
    };

Now it makes sense!

### Creating a function on the fly

We’ve been told over and over again that eval is evil. If you believe this,
the following technique is just as bad:

    // old way
    var rand = eval("var rand = function () { return Math.random() }");

    // ninja way
    var rand = new Function("return Math.random()");

Notice we’re using the Function constructor with a capital F.

### Casting a number literal to a string

When calling toString on a number literal, the number must be wrapped in
parentheses so the JavaScript parser doesn’t interpret the dot as part of a
floating point number. But there are two ways around this major inconvenience
(also thanks to [JavaScript Garden][1]):

    // old way
    (123).toString();

    // ninja way
    123..toString(); // extra dot!
    123 .toString(); // space!

### Entering the void

Who needs _undefined_? Avoid it with _void_:

    // old way
    var val = undefined;

    // ninja way
    var val = void 0;

[1]: http://bonsaiden.github.com/JavaScript-Garden
[2]: /blog/2011/04/06/understanding-bitwise-operations-in-javascript/