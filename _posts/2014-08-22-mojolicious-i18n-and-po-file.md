---
layout: post
title: "Mojolicious I18N and po file"
description: ""
category: "Perl"
tags: ["perl", "Mojolicious", "I18N"]
---
{% include JB/setup %}

The example in [Mojolicious::Plugin::I18N](https://metacpan.org/pod/Mojolicious::Plugin::I18N) is that you put all your translations into *our %Lexicon*.

but sometimes you got .po files from standard I18N tools like gettext. in that case you can do something like below to do the trick.

just create MyApp::I18N

    package MyApp::I18N;

    use base 'Locale::Maketext';
    use File::Basename qw/dirname/;
    use Locale::Maketext::Lexicon {
        _auto => 1,
        _decode => 1,
        '*' => [Gettext => dirname(__FILE__) . '/I18N/*.po']
    };

    1;

that's all you need do. the path above is using lib/MyApp/I18N/*.po, you can change it to somewhere that you put the .po files.

another point is that if you want just do [% l('Hello') %] instead of [% c.l('Hello') %] in TT2, you just put

    $c->render(template => 'template_name', handler => 'tt', l => sub {
        $c->l(@_);
    });

That's it. Enjoy!

