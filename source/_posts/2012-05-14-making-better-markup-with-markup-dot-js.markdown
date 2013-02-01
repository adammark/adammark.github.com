---
layout: post
title: "Making better markup with Markup.js"
date: 2012-05-14 17:40
comments: true
categories: [App Cloud, JavaScript, Markup.js]
---

Unlike traditional web sites, [App Cloud][1] apps compose HTML strings in the
client using JavaScript. There are two ways to go about this: a _good way_ and
a _bad way_.

First, the _bad way_. Consider the following code, in which an array of articles
is manually formatted into a chunk of HTML code:

    var html = "<ul>";

    for (var i = articles.length - 1; i >= 0; i--) {
        html += "<li>";
        html += "<div>" + articles[i].title.toUpperCase() + "</div>";
        html += "<small>";
        html += articles[i].description.substr(0, 50);
        if (articles[i].description.length > 50) { 
            html += "...";
        }
        html += "</small>";
        html += "</li>";
    }

    html += "</ul>";

Notice how even simple tasks, like adding an ellipsis to descriptions longer
than 50 words, can force you to write a lot of code. This gets messy fast!

Now, the _good way_: Take the same array of articles and generate the
equivalent HTML using [Markup.js][2]:

{% raw %}
    <ul>
        {{articles|reverse}}
            <li>
                <div>{{title|upcase}}</div>
                <small>{{description|chop>50}}</small>
            </li>
        {{/articles}}
    </ul>
{% endraw %}

Much nicer! As you can see, Markup.js takes the pain out of converting
structured data (like an array of articles) into HTML or another text format.
And since it's part of the App Cloud SDK, you can quickly and easily separate
your _presentation logic_ from your _business logic_. Let's say you're
handling the results of a data request:

    function handleData(data) {
        var template = bc.templates["articles-list-template"];
        var context = { articles: data };
        var markup = Mark.up(template, context);
        
        document.getElementById("results").innerHTML = markup;
    }

In the above code, Markup.js takes a template string, injects it with a
`context` object, and returns a new string. The new string is then inserted into
the document. There's no HTML at all in your JavaScript code! (You could
easily modify this code to select one of several templates based on a runtime
condition or device characteristic.)

Notice the object `bc.templates`? It's populated automatically with strings
from an external text file (as defined in manifest.json):

    ===== hello-template
    <p>Hello, <span class="username">{{user.name}}!</span></p>

    ===== goodbye-template
    <p>Goodbye, <span class="username">{{user.name}}!</span></p>

In this example, the text file contains two Markup templates: `hello-template`
and `goodbye-template`. You can call them by name, as shown above.

Markup.js comes with more than 40 built-in "pipes" for transforming data, and
it's easy to write your own. Check out the [complete docs][2] on GitHub.

[1]: http://appcloud.brightcove.com
[2]: https://github.com/adammark/Markup.js