---
layout: post
title: "Net::Telnet with bitflu"
description: ""
category: perl
tags: ['perl']
---
{% include JB/setup %}

Even [Net::Telnet](https://metacpan.org/module/Net::Telnet) is quite old, it's still very powerful and simple to use.

    use strict;
    use warnings;
    use Net::Telnet ();
    use Data::Dumper;

    my $host = '0';
    my $port = 4001;

    my $telnet = Net::Telnet->new();
    unless ($telnet->open( Host => $host, Port => $port, Timeout => 30 )) {
        die "Can't connect to $host:$port\n";
    }

    $telnet->waitfor('/bitflu> /');

    my @messages = map { chomp; $_ } $telnet->cmd(String => 'ls');
    pop @messages if $messages[-1] eq 'bitflu';
    print Dumper(\@messages);

    $telnet->close();

there are some tips:

#### remove ANSI color

    foreach my $msg (@messages) {
        # if you do not remove this, your regex with /^\[/ may break
        $msg =~ s/\e\[[\d;]*[a-zA-Z]//g;
    }

#### Change Window Size

if you use term to do bitflu> ls, you'll see full torrent name. but with the code above, you can only see few chars. here is the note to change the Window Size:

    my $telnet = Net::Telnet->new();

    $telnet->option_callback( sub { return; } );
    $telnet->option_accept(Do => 31);

    unless ($telnet->open( Host => $host, Port => $port, Timeout => 60 )) {
        die "Can't connect to $host:$port\n";
    }
    $telnet->waitfor('/bitflu> /');

    ## copied from http://blog.webdir.bg/perl-apache-realtime-output-from-script/
    ## Many Thanks!
    $telnet->telnetmode(0);
    $telnet->put(pack("C9",
                      255,                  # TELNET_IAC
                      250,                  # TELNET_SB
                      31, 0, 200, 0, 0,     # TELOPT_NAWS
                      255,                  # TELNET_IAC
                      240));                # TELNET_SE
    $telnet->telnetmode(1);
