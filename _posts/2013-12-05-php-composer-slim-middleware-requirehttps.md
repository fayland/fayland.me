---
layout: post
title: "PHP Composer, Slim Middleware RequireHTTPS"
description: ""
category: "php"
tags: ["php", "composer", "Slim"]
---
{% include JB/setup %}

Well, I'm not a fan or expert of PHP. I do not use PHP a lot and I do not know PHP well.

but when I come to write a PHP website, my first pick is always [Slim](http://www.slimframework.com/). it's very lightweight and fits my needs well.

Today I got a needs to redirect all http to https for a website written by Slim, and come out as a new VERY SIMPLE middleware [Slim-Middleware-RequireHTTPS](https://github.com/fayland/Slim-Middleware-RequireHTTPS).

the usage is quite simple:

	$app = new \Slim\Slim();
	$app->add(new \Slim\Middleware\RequireHTTPS());

and that's all. now all http:// will be redirected to https://

Slim uses [composer](http://getcomposer.org/) inside, so I think it's better put my package as a part of composer too. I spent few minutes to check how to write composer.json (copied from slim one) and get it into the [Packagist](https://packagist.org/packages/fayland/slim-middleware-requirehttps) in next few minutes.

I was amazed by the progress at some points. damn, CPAN is really very old fashion (BUT it works GOOD.).

first, submit a new package is simply type a URL. and it will read all the info from remote composer.json. dead simple.

since that's git (or other VCS), version is simply supported with --tags. you do git tag -a X.Y and with hook in github repos settings, the version will be shown up in the website immediately. and there is always dev-master which maps to the master source code.

Packagist does not need host any files. when you go composer install/update, it fetches from the remote VCS. really smart idea.

Have fun.
