---
layout: post
title: "Mojolicious TT2 patch"
description: ""
category: perl
tags: ['Mojolicious', 'TT2']
---
{% include JB/setup %}

I am kindy busy with [adding new features](https://github.com/fayland/findmjob.com/commits/master) to my [job site](http://findmjob.com/)

but it's very boring to restart the app on template updates. TT2 should be able to pick up the changes automatically. it works under Dancer or Catalyst, but not Mojolicious.

I thought I should spend some time on investigating why before writing more stuff. and after a while, I have [a patch](https://github.com/fayland/mojox-renderer-tt/commit/d15192619713b044878301c6f911df4c27aa0d84) for [Mojolicious::Plugin::TtRenderer](https://github.com/plicease/mojox-renderer-tt).

it dues to the Provider in TtRender always return 1 instead of *mtime* on `_template_modified`.

plicease accepts it quite fast with slight changes but I'm waiting for a CPAN release. :-)

here is few changes on [http://findmjob.com/](http://findmjob.com/) recently.

* tag view is splitted with [job](http://findmjob.com/tag/OOm8jHZ84RGjYrDhKQ5yzw/+job/perl.html) and [freelance](http://findmjob.com/tag/OOm8jHZ84RGjYrDhKQ5yzw/+freelance/perl.html).

* Location link is added like: [San Francisco, CA](http://findmjob.com/location/wM4xraui4hGi3+CgdEa_Ag/San-Francisco-CA.html)

Happy hacking!
