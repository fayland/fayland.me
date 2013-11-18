---
layout: post
title: "cpan-count nodejs module"
description: ""
category: "javascript"
tags: ["nodejs", "CPAN", "coffeescript"]
---
{% include JB/setup %}

It is my first [npm module](https://npmjs.org/package/cpan-count). it is a nodejs module to get the modules count of one CPAN author thourgh [MetaCPAN](http://metacpan.org/) API. it is quite simple because it's almost a copy-paste from the [gem-count](https://github.com/eighttrackmind/gem-count). but at last, it's still very interesting and fun to learn some nodejs and try *npm publish*

few points:

 * it takes a while for me to find out the cpan-count api call as http://api.metacpan.org/v0/author/:user?join=release&q=release.status:latest
 * I have also contributed a pull request to the author of [contributor.io](https://github.com/fayland/contributor.io/commit/88eb1ad55ace8f3ba27f0df7edb01b828d35a442)
 * npm register and publish is so damn simple that I haven't imagined. sign up on the web costs less than 1 minute. `npm adduser` costs less than 1 minute. `npm publish .` costs less than 1 minute. and MY MODULE SHOWS UP AT THE WEBSITE costs less than 1 minute.
 * I like the package.json, I know Perl has META.yml or META.json but package.json has two points I like, one is you do not define version in somewhere else (Perl need write it in the main module also. that's why dzil is so popular because it saves time.) and it contains keywords. keywords is good for search.

Have fun.
