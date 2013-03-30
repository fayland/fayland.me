---
layout: post
title: "Two new CPAN modules"
description: ""
category: perl
tags: ['perl', 'CPAN']
---
{% include JB/setup %}

I got two new CPAN modules uploaded today.

### [WWW::SpinnerChief](https://metacpan.org/module/WWW::SpinnerChief)

I wrote this based on the [Python code](https://github.com/niteoweb/spinnerchief/blob/master/src/spinnerchief/__init__.py)

it's pretty good that you know how to read the Python.

### [Business::PayPoint](https://metacpan.org/module/Business::PayPoint)

aka tips to write SOAP module in Perl.

the PHP SOAP lib is pretty good while the Perl one is a little suck.

so usually if I can't write it at the first try in Perl, I would use PHP to find the sending request/response

    $client = new SoapClient('https://www.example.com/Test?wsdl', array(
        'trace' => 1,
    ) );
    $client->__call('TestAction', $params);
    echo "RESPONSE:\n" . $client->__getLastResponse() . "\n";
    echo "REQUEST HEADER:\n" . $client->__getLastRequestHeaders() . "\n";
    echo "REQUEST:\n" . $client->__getLastRequest() . "\n";

After I got the correct sample request, I'll try to use Perl library to send the same XML with trace on.

    use SOAP::Lite +trace => 'all';

well, you even can't write correct one sometimes (maybe I am a little stupid).

but I have a final trick for it. use XML::Write to genereate the request XML. then use

    my $som = $soap->call($method, SOAP::Data->type('xml' => $xml));

you won't be wrong in this case. :)

Have fun.