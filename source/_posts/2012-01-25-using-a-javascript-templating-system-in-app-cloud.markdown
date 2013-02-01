---
layout: post
title: "Using a JavaScript templating system in App Cloud"
date: 2012-01-25 17:24
comments: true
categories: [App Cloud, JavaScript, Markup.js]
---

In a typical web application, a web server is largely responsible for
compiling HTML code before sending it to the client. This can be done with
languages like PHP, Java and Ruby. But in an [App Cloud][2] app, HTML is
compiled in the client with the help of JavaScript. For example, building up a
list of blog entries:

    var html = "<ul>";
    for (var i = 0; i < results.length; i++) {
        html += "<li><b>" + results[i].title.toUpperCase() + ":</b> "
             + results[i].desc + "</li>";
    }
    html += "</ul>";

This can get ugly fast. Enter JavaScript templating systems. A _templating
system_ compiles HTML code for you—all it needs is a template (string) and some
context data (a JavaScript object). Here's what a template might look like:

{% raw %}
    <ul>
        {{articles}}
            <li><b>{{title|upcase}}:</b> {{desc}}</li>
        {{/articles}}
    </ul>
{% endraw %}

Easier to read, right? And definitely easier to write!

There are plenty of JavaScript templating systems, including Mustache, jQuery
Templates, and [Markup.js][1], which I created with App Cloud in mind. The
above example is from Markup.js. So how do we actually populate a template
with context data?

    var context = {
        name: {
            first: "John",
            last: "Doe"
        }
    };
    var template = "Hi, {{name.first}}!";
    var markup = Mark.up(template, context); // "Hi, John!"

The resulting string can then be injected into your HTML document.

In an App Cloud app, the context data is likely to come from a content feed.
For example:

    bc.core.getData("blog",
        function (data) {
            var template = bc.templates["article-index"];
            var context = { articles: data };
            var markup = Mark.up(template, context);

            document.getElementById("blog-results").innerHTML = markup;
        },
        function (error) {
            bc.device.alert("Oops! " + error.errorMessage);
        }
    );

Markup.js also supports control logic (if/else), loops, and "pipes" for
transforming variables. Check out the [full documentation][1] on GitHub.

[1]: https://github.com/adammark/Markup.js
[2]: http://appcloud.brightcove.com