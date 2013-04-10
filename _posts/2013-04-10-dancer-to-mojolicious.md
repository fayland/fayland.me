---
layout: post
title: "Dancer to Mojolicious"
description: ""
category: perl
tags: ['Dancer', 'Mojolicious']
---
{% include JB/setup %}

The progress went smoothly because all of them are just Perl code.

old [Dancer](http://www.perldancer.org/) code: [FindmJob::WWW](https://github.com/fayland/findmjob.com/blob/3368b812b72d11cbd1534d2cb870ad0f331a0bf7/www/lib/FindmJob/WWW.pm)

new [Mojolicious](http://mojolicio.us/) code:
[FindmJob::WWW](https://github.com/fayland/findmjob.com/blob/5727a9f68cca0d18bf7acb26b7ccaa9ab05663b1/lib/FindmJob/WWW.pm), [FindmJob::WWW::Root](https://github.com/fayland/findmjob.com/blob/5727a9f68cca0d18bf7acb26b7ccaa9ab05663b1/lib/FindmJob/WWW/Root.pm) and [others](https://github.com/fayland/findmjob.com/tree/5727a9f68cca0d18bf7acb26b7ccaa9ab05663b1/lib/FindmJob/WWW)

### Few notes

#### hooks

from `before_template_render` to `before_render`

#### Dancer `forward` VS Mojolicious `before_dispatch`

we can modify the req->url->path in `before_dispatch` with assigning stash.

    # feed.(rss|atom) and /p.2/
    $self->hook( before_dispatch => sub {
        my $self = shift;

        my $p = $self->req->url->path;
        if ($p =~ s{/feed\.(rss|atom)$}{}) {
            $self->stash('is_feed' => $1);
        }
        if ($p =~ s{/p\.(\d+)(/|$)}{$2}) {
            $self->stash('page' => $1);
        }
        $self->req->url->path($p);
    });

#### supervise

Dancer:

    plackup -E production -s Starman --workers=3 -l /tmp/findmjob.sock -a /findmjob.com/www/bin/app.pl

Mojolicious:

    hypnotoad -f /findmjob.com/bin/www.pl

Note `-f` is important here, or supervise will keep restarting the script.

above plackup using sock and hypnotoad use port. so we need update the ngnix config a bit.

and it looks like hypnotoad is working better than plackup Starman

#### Template name conversation

there is no rule in Dancer for the Template name. but in Mojolicious, we have to do it with $name.$format.$handler

in this case we have to rename index.tt2 to index.html.tt

### Conclusion

well, I'm not saying that Dancer is worse than Mojolicous or any other words. both of them are great.

but Dancer is a bit messy with Dancer and Dancer2. actually I love Moo a lot, but I don't want to spend time on upgrading Dancer to Dancer2 (there seems some more difference than expected.)

in the other hand, Mojolicious looks amazing, sri improves it every week and I admire/trust his professional knowledge.

Have fun.
