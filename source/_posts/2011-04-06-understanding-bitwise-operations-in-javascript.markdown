---
layout: post
title: "Understanding bitwise operations in JavaScript"
date: 2011-04-06 23:20
comments: true
categories: [JavaScript]
---

I’ve been reading [Code: The Hidden Language of Computer Hardware and Software][1]
by Charles Petzold. It’s a great introduction to the building blocks of 
computer science—_ones and zeros_—for the liberal arts majors among us. 
Check it out and you’ll understand this joke:

> There are only 10 kinds of people in the world: Those who understand binary
> and those who don’t.

When you’re done ROFLing, consider some of the ways you can use bitwise
operations in everyday JavaScript code:

## Use a bitmask to check for inclusion in a set

Say you’ve got a bowl of five different fruits and you want to know if it
contains a banana. You could simply check every piece of fruit in the bowl to
see if it’s a banana:

    function contains(bowl, fruit) {
        for (var i = 0; i < bowl.length; i++) {
            if (bowl[i] == fruit) {
                return true;
            }
        }

        return false;
    }

    // has banana? yes
    contains(["apple", "banana", "cherry"], “banana”);

Or you could use `Array.indexOf` to get the same result:

    function contains(bowl, fruit) {
        return bowl.indexOf(fruit) > -1;
    }

    // has banana? yes
    contains(["apple", "banana", "cherry"], “banana”);

    // has banana? no
    contains(["apple", "grape", "cherry"], “banana”);

But what if you want to know whether the bowl contains a banana, a cherry and
an apple?

    var bowl = ["apple", "banana", "cherry", "grape", "peach"];

    // has banana, cherry and apple? yes
    contains(bowl, “banana”) && contains(bowl, “cherry”) && contains(bowl, “apple”);

This gets ugly fast. You could, of course, modify the `contains` function to
accept an array of fruits:

    function contains(bowl, fruits) {
        for (var i = 0; i < fruits.length; i++) {
            if (bowl.indexOf(fruits[i]) == -1) {
                return false;
            }
        }

        return true;
    }

    var bowl = ["strawberry", "grape", "peach", "orange"];

    var fruits = ["banana", "cherry", "apple"];

    // has banana, cherry and apple? no
    contains(bowl, fruits);

That’s better, but let’s try doing it without arrays and loops. Enter
bitmasks! First, assign each possible option a value of 2 to the power of n,
starting with n=0:

    var Fruit = {
        BANANA:       1,
        ORANGE:       2,
        STRAWBERRY:   4,
        PEACH:        8,
        APPLE:       16,
        GRAPE:       32,
        CHERRY:      64,
        TANGERINE:  128
    };

Each decimal value converts to a binary sequence that contains exactly one
“1.” For example, ORANGE equals 10 and STRAWBERRY equals 100. Together they
equal 110:

       010
    OR 100
       —
       110

You can quickly calculate the sum of the bowl using a bitwise OR expression.
Say the bowl has a banana, a peach and a tangerine:

    var bowl = Fruit.BANANA | Fruit.PEACH | Fruit.TANGERINE;

This bowl equals 137 in decimal or 10001001 in binary. Notice the number of
ones in the result equals the number of fruits in the bowl:

       00000001  BANANA
    OR 00001000  PEACH
    OR 10000000  TANGERINE
       ——–
       10001001

Now you can represent any configuration of eight fruits in just eight digits!

The resulting value, 10001001, will serve as a bitmask to determine whether
the bowl contains certain fruits. Testing for the presence of a single fruit
is straightforward with a bitwise AND:

        10001001  BOWL
    AND 00000001  BANANA
        ——–
        00000001  TRUE

        10001001  BOWL
    AND 00000010  ORANGE
        ——–
        00000000  FALSE

Now just check to see if bowl AND fruit is greater than zero:

    function contains(bowl, fruit) {
        return (bowl & fruit) > 0;
    }

    var bowl = Fruit.BANANA | Fruit.PEACH | Fruit.TANGERINE;

    // has banana? yes
    contains(bowl, Fruit.BANANA);

Testing for the presence of multiple fruits is a bit trickier but just as
elegant. Since the ANDed value can be positive if just some of the fruits are
present, you need to make sure the ANDed value is greater than or equal to the
value of fruits itself:

    function contains(bowl, fruits) {
        return (bowl & fruits) >= fruits;
    }

    var bowl = Fruit.BANANA | Fruit.PEACH | Fruit.TANGERINE;

    // has banana and tangerine? yes
    contains(bowl, Fruit.BANANA | Fruit.TANGERINE);

    // has banana and apple? no
    contains(bowl, Fruit.BANANA | Fruit.APPLE);

See how the bitmask method performs against the array method at [jsperf.com][2].

## Use bitwise AND for alternation

You’ve probably used a [modulus][3] to test whether the value of a counter
is odd or even:

    for (var i = 0; i < 10000; i++) {
        if (i % 2 == 0) {
            // even
        }
        else {
            // odd
        }
    }

But in big loops it’s faster to use a binary AND expression. In binary, an
even number AND 1 is always 0 (even), while an odd number AND 1 is always 1
(odd):

    for (var i = 0; i < 10000; i++) {
        if (i & 1 == 0) {
            // even
        }
        else {
            // odd
        }
    }

## Use bitwise shifting to convert hexadecimal values

Did you ever wonder what “hex” (base 16) color values look like in another
number system? Take the value of pure red: FF0000. In decimal (base 10) it’s
16711680 and in binary (base 2) it’s 111111110000000000000000. Try it for
yourself in a JavaScript console:

    0xFF0000.toString(10);
    0xFF0000.toString(2);

Now let’s say you want to convert the hex value to RGB, in which R, G and B
are values ranging from 0 to 255:

    function hexToRGB(hex) {
        var r = (hex & 0xFF0000) >> 16;
        var g = (hex & 0x00FF00) >> 8;
        var b = (hex & 0x0000FF);
        return [r,g,b];
    }

Here, the inputted value is being ANDed with the values of pure red, green and
blue, then the red and green values are shifted to the right by 16 bits and 8
bits, respectively. The result is three 8-bit values, or 0-255 in decimal.

Take the color gold: 0xFFCC00. What are the individual RGB values?

    // returns [255, 204, 0]
    var rgb = hexToRGB(0xFFCC00);

And it works the other way around. For example, to create a hex string from
red, blue and green values:

    function rgbToHexString(r, g, b) {
        var color = (r << 16) | (g << 8) | b;
        return “#” + (“000000″ + color.toString(16)).substr(-6);
    }

    // returns “#ffcc00″
    rgbToHexString(255, 204, 0);

As you can see, binary operations are useful for everyday JavaScript
programming tasks. And they’re super fast!

[1]: http://amzn.com/0735611319
[2]: http://jsperf.com/array-search-vs-bitmask-search
[3]: https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Operators/Arithmetic_Operators#.25_.28Modulus.29
