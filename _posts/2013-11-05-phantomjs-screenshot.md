---
layout: post
title: "phantomjs screenshot"
description: ""
category: "javascript"
tags: ["javascript", "phantomjs"]
---
{% include JB/setup %}

write test.js

{% highlight javascript %}

var page = require('webpage').create();

page.viewportSize = { width: 1024, height: 800 };
page.clipRect = { top: 0, left: 0, width: 1024, height: 800 };
page.open('http://findmjob.com/', function () {
    page.render('findmjob.png');
    phantom.exit();
});

{% endhighlight %}

then do

	phantomjs test.js

I found this tool from [Wight](https://github.com/motemen/Wight) and it's pretty amazing.

I'll play it a bit more and share if something is interesting.