---
layout: post
title: "phantomjs/casperjs and qiandao"
description: ""
category: "javascript"
tags: ["phantomjs", "casperjs", "coffeescript"]
---
{% include JB/setup %}

Well, qiandao here means Chinese 签到。

that action is boring that you need open browser, login, then click buttons. afterwards, you get some points that you can use it somehow as a little money.

Programming is born for saving you from daily repeating/boring works. and that's why programming is fun.

I spent few hours to write a casperjs coffeescript today to do the action for taobao.com/etao.com. the code is quite simple and the result is very interesting. phantomjs or casperjs is born for suck work.

you can take a look of the code at [https://github.com/fayland/casperjs-qiandao/blob/master/taobao.coffee](https://github.com/fayland/casperjs-qiandao/blob/master/taobao.coffee), it's quite self-explaining. open page, click button, wait until frame shows, type user/pass, then submit. afterwards, just wait until the result shows up. and print it. meanwhile, after collect few 淘金币, it also collects one 集分宝.

crontab it as casperjs /path/to/casperjs-qiandao/taobao.coffee --username=fayland_lam --password=secret

and that's it. programming does the job for you and it's reliable.

have fun.