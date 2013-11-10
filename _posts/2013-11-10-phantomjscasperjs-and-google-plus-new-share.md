---
layout: post
title: "phantomjs/casperjs and google plus new share"
description: ""
category: "javascript"
tags: ["javascript", "phantomjs", "casperjs"]
---
{% include JB/setup %}

phantomjs is great. the wrapper [casperjs](http://casperjs.org/) is even better.

when surfing around for a Google+ poster as what I did for [Twitter/Facebook/Linkedin](https://github.com/fayland/findmjob.com/tree/master/cron/sharebot/lib/FindmJob/ShareBot) etc., I find amazing [altryne/google-plus-api](https://github.com/altryne/google-plus-api)

it use casperjs and it's very simple to use.

just one tiny issue, it does not use cookie and logins every time. so I made a [small patch](https://github.com/fayland/google-plus-api/commit/ff21daa956b6f79b4dcd9e671a889973f686e604) for that, and send the pull request to the author.

I'll merge it into [findmjob.com](http://findmjob.com/) soon. you'll find fresh job posting on [Findmjob Google+](https://plus.google.com/u/0/108951842434983124305/posts).

Have fun.