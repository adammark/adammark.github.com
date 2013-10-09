---
layout: post
title: "JavaScript tricks to impress your friends"
date: 2011-08-11 17:56
comments: true
categories: [JavaScript]
---

I recently came across some mind-bending JavaScript shortcuts in a web project
I inherited from another developer. Most of these techniques are bad from a
readability perspective—and none of them offer significant performance
gains—but you should feel free to discuss them at cocktail parties to impress
your friends.

### Casting a string to a number

Use the unary plus operator to cast a string to a number:

    // old way
    parseInt("123", 10); // 123
    parseFloat("45.678"); // 45.689
    Number("9"); // 9

    // ninja way
    +"123.45"; // 123.45

Note parseInt() and parseFloat() are actually more versatile:

    parseInt("123px", 10); // 123
    +"123px"; // NaN

    parseFloat("45.678deg"); // 45.678
    +"45.678deg"; // NaN

### Convert a date to UTC milliseconds

Use the unary plus operator to cast a Date object to milliseconds since the Unix epoch:

    var date = new Date(); // Thu Aug 11 2011 10:47:37 GMT-0400 (EDT)

    // old way
    date.getTime(); // 1313074057920
    date.valueOf(); // 1313074057920

    // ninja way
    +date; // 1313074057920

### Testing for a substring with bitwise NOT

Use the bitwise NOT operator to test for the presence of a substring:

    // old way
    "Hahaha".indexOf("ha") > -1; // true

    // ninja way
    ~"Hahaha".indexOf("ha"); // true

Wait, what? The bitwise NOT (or complement) of a signed integer is equal to
the negative of that number minus 1:

    ~2 = -3; // resolves to true
    ~0 = -1; // also true
    ~-1 = 0; // false

This is kind of nuts, but it does save you from typing about four extra
characters.

### Testing for the presence of a value

Use a double NOT (or "bang bang") to test if a variable value is not null, not
undefined and not an empty string:

    var name = "Adam";

    // old way
    name != null && name != undefined && name != ""; // true

    // ninja way
    !!name; // true

The first bang casts the value to a Boolean and the second bang negates it. In
the ninja example above, the expression resolves to !false, or true.

### Preempting a function call

Create a boolean expression to avoid calling a function if the function value
is undefined:

    // old way
    var handleResponse = function (data, callback) {
        if (callback) {
            callback(data);
        }
    }

    // ninja way
    var handleResponse = function (data, callback) {
        callback && callback(data);
    }

In the ninja example above, if the the first half of the Boolean test is false or undefined, the second half is never evaluated.

### Chaining function calls

Variables are for suckers! If one function returns another, you can just
execute the returned function right away:

    var stack = [function1, function2, function3];

    // old way
    var func = stack.pop();
    func();

    // ninja way
    stack.pop()();

### Concatenating strings

The plus sign: also for suckers. Use an array to join string fragments:

    // old way
    var name = "A" + "d" + "a" + "m";

    // ninja way
    var name = ["A", "d", "a", "m"].join("");
