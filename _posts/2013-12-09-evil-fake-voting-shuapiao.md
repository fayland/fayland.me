---
layout: post
title: "evil fake voting: shuapiao"
description: ""
category: "perl"
tags: ["perl"]
---
{% include JB/setup %}

Some days ago, one of my relatives asks me if I know how to do fake votings. she has a niece who wants to be a cover girl of the calendar.

Yes. I know it's evil. but as I know, some people are also doing that. so we have no choice somehow.

for fake voting, there are two requirements. one is you need lots of IPs (Tor is not changing IP fastly and not reliable on such task). the other is you need do some decaptcha to prove you're not a robot (actually that's a robot).

I won't tell you how to rent lots of IPs. but the decaptcha service, I recommend the [DeathByCaptcha](http://deathbycaptcha.com/), it's quite cheap and reliable on most of the time.

I published the code at github, that you can [take a look](https://github.com/fayland/shuapiao/blob/master/rarb.cn/voting.pl)

that's a simple Perl script, nothing magic. here are few tips:

 * use WWW::UserAgent::Random to change user agent so that it looks like not from one user.
 * use Parallel::ForkManager to do the forks. +1 every minute is not fast, you can't beat others.

otherwise, all are simple and you're welcome to use that as a start for a new fake voting script.

have fun.