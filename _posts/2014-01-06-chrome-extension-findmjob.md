---
layout: post
title: "Chrome Extension: Findmjob"
description: ""
category: "javascript"
tags: ["javascript", "chrome", "extension"]
---
{% include JB/setup %}

I just got my first Chrome Extension published: [Findmjob: Push Jobs to You](https://chrome.google.com/webstore/detail/findmjob-push-jobs-to-you/ogknnjoiljfafebechhnjgjommbolhoa)

the basic was created with [Extensionizr](http://extensionizr.com/). it's a very useful tool.

the source is at [https://github.com/fayland/findmjob.com_chrome_extension](https://github.com/fayland/findmjob.com_chrome_extension)

it's pure javascript. use localStorage to store the options data and transfer data from background.js to browser_action.js (need JSON parse and stringify since it only accept strings.)

Notification is quite simple as below:

    var notification = window.webkitNotifications.createNotification(
        '../../icons/icon48.png',            // The image.
        v.title,                       // The title.
        v.title      // The body.
    );
    notification.onclick = function() { // Open on click
        window.open(base_url + v.url + '?' + REF_STRING);
        notification.cancel();
    }
    notification.show();
    // Close after 20 secs
    setTimeout(function() {
        notification.cancel();
    }, 20 * 1000);

and Badge Text in browserAction:

    chrome.browserAction.setBadgeText({
        text: data.updates.length.toString()
    });

super simple. and works great.

Enjoy.