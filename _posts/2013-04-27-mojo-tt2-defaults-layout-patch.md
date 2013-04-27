---
layout: post
title: "mojo tt2 defaults layout patch"
description: ""
category: perl
tags: ["Mojolicious", "TT2"]
---
{% include JB/setup %}

You wrote code with open source like CPAN. You meet problems with them. You investigate, write tests then provide patches. Your patches are accepeted.

I really enjoy the way it moves.

Here is [another patch](https://github.com/fayland/mojox-renderer-tt/commit/95d9ee5c356fa3f398b2deed9611ba47b69a890b) for [Mojolicious::Plugin::TtRenderer](https://github.com/plicease/mojox-renderer-tt).

the issue is that `$self->defaults(layout => 'wrapper');` is always dropping the `[% content %]` without reason. and with debug I see the content is really in `$c->stash->{'mojo.content'}`. so a simple patch is that just `$c->stash->{content} ||= $c->stash->{'mojo.content'}->{content};`

recently I'm writing another new app with bitcoin <-> litecoin and other virtual coins exchange. and I have a wrapper.html.tt for the whole site. but I do not want to use it in the email TT2 render.

if I put `WRAPPER => 'layouts/wrapper.html.tt',` in the TT2 options, it will also apply to the mail render. a better approach is to use defaults layout. then in email render, set the layout as empty or actually we need use `partial => 1`.

MainApp.pm

	$self->plugin('tt_renderer');
    $self->defaults(layout => 'wrapper');
    $self->renderer->default_handler( 'tt' );

OtherController.pm

	my $body = $c->render(
        template => 'emails/forgot_pass', format => 'mail',
        other_stash => $var,
        partial => 1
    );

partial => 1 will set layout as null. so it will give us what we want.

Have fun!