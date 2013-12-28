---
layout: post
title: "Play with Go Lang"
description: ""
category: "go"
tags: ["Go"]
---
{% include JB/setup %}

Well, few days ago I was a bit free and boring, I started to read a [Go book online](https://github.com/astaxie/build-web-application-with-golang).

you know you'll get nothing until you start coding, so I started my hack on simplest stuff. always get stroke count of a Chinese character. at last, all the code is at [https://github.com/fayland/chinese_stroke](https://github.com/fayland/chinese_stroke)

The whole progress is done by keeping Googling with how to read file with Go, how to replace string, upper case etc. but I'm quite glad that the code is working finally.

the learning is interesting and there are some good points in Go that I like.

 * you can't import a module but do not use it (well, it's quite troublesome that I need keep enable fmt for debugging then disable it on publish anyway)
 * import functions are started with upper case. there are traditions/rules everywhere that makes Go faster.

and something I do not like at all.

 * the type system is pretty killing since I am from a Perl background. I'm good with a type system like Python but Go is really quite trouble when there are string, bytes and rune in strconv.
 * the func return is not that ... you have to use `, _` (to discard the extra values) even we just need one value returned.

Well, it's from a newbie really. I just read Go for just 3 or 4 hours. so bear with it.

Thanks.