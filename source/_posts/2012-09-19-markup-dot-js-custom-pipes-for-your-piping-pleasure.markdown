---
layout: post
title: "Markup.js: Custom pipes for your piping pleasure"
date: 2012-09-19 15:13
comments: true
categories: [App Cloud, Markup.js, JavaScript]
---

While [Markup.js][1] comes with more than 40 built-in pipes for everyday use,
I always write a few custom pipes whenever I build an [App Cloud][2] app. Here
are some of my favorites.

### highlight

Use this pipe to highlight a search term or other pattern in a string. Note
the use of backticks in the example to denote a context variable on the right
side of the expression.

{% raw %}
    // Example: {{article|highlight>`searchTerm`}}

    Mark.pipes.highlight = function (str, pattern) {
        return str.replace(new RegExp("(" + pattern + ")", "g"), "<em>$1</em>");
    };
{% endraw %}

### address

Use this pipe to wrap an address in a Google Maps link.

{% raw %}
    // Example: {{home_addr|address}}

    Mark.pipes.address = function (addr) {
        return "<a href=\"http://maps.google.com/maps?q=" + encodeURI(addr) + ">" + addr + "</a>";
    };
{% endraw %}

### links

Use this pipe to convert all URLs in a string to links.

{% raw %}
    // Example: {{story|links}}

    Mark.pipes.links = function (str) {
        return str.replace(/\b(https?:[^\b\s]+)\b/g, "<a href=\"$1\">$1</a>");
    };
{% endraw %}

### repeat

Use this pipe to repeat a string. Note `count` defaults to 2 and `separator`
defaults to "".

{% raw %}
    // Example: {{chorus|repeat>5}}

    Mark.pipes.repeat = function (str, count, separator) {
        return new Array(+count || 2).join(str + (separator || "")) + str;
    };
{% endraw %}

### moment

Use this pipe to format a date with [Moment.js][3].

{% raw %}
    // Example: {{created_at|moment>M/D/YYYY}}

    Mark.pipes.moment = function (date, format) {
        return moment(new Date(+date || date)).format(format);
    };
{% endraw %}

### dollars

Use this pipe to format a number in dollars with [Accounting.js][4].

{% raw %}
    // Example: {{price|dollars}}

    Mark.pipes.dollars = function (num) {
        return accounting.formatMoney(+num);
    };
{% endraw %}

### phone

Use this pipe to format a U.S. phone number.

{% raw %}
    // Example: {{mobile_phone|phone}}

    Mark.pipes.phone = function (str) {
        var s = str.replace(/[^\d]/g, "");
        return "(" + s.substr(0, 3) + ") " + s.substr(3, 3) + "-" + s.substr(6, 4);
    };
{% endraw %}

### ordinal

Use this pipe to express a number as an ordinal, e.g. "10th".

{% raw %}
    // Example: {{contestant.standing|ordinal}}

    Mark.pipes.ordinal = function (num) {
        if (num > 10 && num < 20) {
            return num + "th";
        }
        return num + ["th","st","nd","rd","th","th","th","th","th","th"][num % 10];
    };
{% endraw %}

### runtime

Use this pipe to express a number in stopwatch notation ("mm:ss") given a
factor of 1 (seconds) or 1000 (milliseconds). Note `factor` defaults to 1.

{% raw %}
    // Example: {{duration|runtime}}

    Mark.pipes.runtime = function (time, factor) {
        var m = Math.floor(time / (60 * (factor || 1)));
        var s = Math.floor((time / (factor || 1)) % 60);
        return m + ":" + ("00" + s).substr(-2);
    };
{% endraw %}

### has

Use this pipe to determine if an array contains an object with the given
property value.

{% raw %}
    // Example: {{if fruits|has>color>red}} ... {{/if}}

    Mark.pipes.has = function (arr, prop, val) {
        return arr.some(function (item) {
            return item[prop] == val;
        });
    };
{% endraw %}

### sift

Use this pipe to filter an array of objects to only those having the given
property value.

{% raw %}
    // Example: <ul> {{fruits|sift>color>red}} <li>{{fruit.name}}</li> {{/fruits}} </ul>

    Mark.pipes.sift = function (arr, prop, val) {
        return arr.filter(function (item) {
            return item[prop] == val;
        });
    };
{% endraw %}

### stars

Use this pipe to print star and half-star characters given a decimal input.
Note this requires [Font Awesome][5].

{% raw %}
    // Example: {{rating|stars}}

    Mark.pipes.stars = function (rating) {
        var n = Math.round(+rating * 2) / 2;

        return new Array(Math.floor(n) + 1).join("&#xf005;") + (n % 1 ? "&#xf089;" : "");
    };
{% endraw %}

Get more pipes in the [Markup.js][1] repository on GitHub.

[1]: https://github.com/adammark/Markup.js
[2]: http://appcloud.brightcove.com
[3]: http://momentjs.com/
[4]: http://josscrowcroft.github.com/accounting.js/
[5]: http://fortawesome.github.com/Font-Awesome/