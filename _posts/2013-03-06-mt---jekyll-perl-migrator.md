---
layout: post
title: "MT  > Jekyll perl migrator"
description: ""
category: perl
tags: ['perl', 'Jekyll', 'MovableType5']
---
{% include JB/setup %}

I bought a new domain [fayland.me](http://fayland.me/).

I picked [Jekyll](https://github.com/mojombo/jekyll) as the blog engine.

I wrote a simple Perl script to convert my old Movable Type 5 blogs to Jekyll Bootstrap.

[Github code](https://github.com/fayland/p5-jekyll-scripts/blob/master/mt/migrator.pl)

the difference between this one and the [Jekyll::MT](https://github.com/mojombo/jekyll/wiki/blog-migrations) is that it supports tags and it's for [Jekyll Bootstrap](http://jekyllbootstrap.com/).

at last, using

    rsync -arv --delete _site fay:/srv/www/fayland.me/

to rsync the site.

Have fun.