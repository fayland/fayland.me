---
layout: post
title: "Mojolicious basic_auth and DBIx::Class JSON InflateColumn::Serializer"
description: ""
category: "perl"
tags: ["Mojolicious", "DBIx::Class", "perl"]
---
{% include JB/setup %}

Well, it's very good that you have something to work or hack. yesterday I was working to add some new features to my toy website [http://findmjob.com/](http://findmjob.com/)

I decided to add an admin interface which will use basic_auth to protect.

[Mojolicious::Plugin::BasicAuth](https://metacpan.org/pod/Mojolicious::Plugin::BasicAuth) fits the need well but it does not have a good example really. I do want to put it under a whole site or certain path instead of write it everywhere. so here is the [sample code](https://github.com/fayland/findmjob.com/blob/master/lib/FindmJob/WWWAdmin.pm)

{% highlight perl %}
    $self->plugin('basic_auth');
    $r = $r->under(sub {
        my $self = shift;
        unless ( $self->basic_auth( realm => sub { return 1 if "@_" eq $config->{admin}->{auth} } ) ) {
            $self->render(text => 'Permission Denied.');
            return 0;
        }
        return 1;
    });
{% endhighlight %}

another story is for DBIx:Class InflateColumn::Serializer. well, I use DBIx::Class::Schema::Loader to create the Result Tables.pm. which means that I can't hack the add_columns as suggested in the [POD](https://metacpan.org/pod/DBIx::Class::InflateColumn::Serializer). by checking the source, I know I can do it somehow like

    use DBIx::Class::InflateColumn::Serializer::JSON;
    __PACKAGE__->inflate_column(
        data => {
            inflate => DBIx::Class::InflateColumn::Serializer::JSON->get_unfreezer('data'),
            deflate => DBIx::Class::InflateColumn::Serializer::JSON->get_freezer('data'),
        }
    );

but that's too damn weird and not looks good. so instead, I start writing a patch for that module so that it can be also written as:

    __PACKAGE__->load_components('InflateColumn::Serializer');
    __PACKAGE__->set_serialize_column('data', 'JSON');

the patch is [here](https://github.com/fayland/DBIx-Class-InflateColumn-Serializer/commit/d539f2992195113821a565393bfeda6ba3e4f04b). hope that it can be merged soon.

Happy Hacking.

*Updated on Dec 28th*

the patch is really not useful. the Author [pointed out](https://github.com/miquelruiz/DBIx-Class-InflateColumn-Serializer/pull/1#issuecomment-31262782) that we can do it like below:

    __PACKAGE__->load_components('InflateColumn::Serializer');
    __PACKAGE__->add_columns('+data', { serializer_class => 'JSON' });

which is much more cleaner. Thanks