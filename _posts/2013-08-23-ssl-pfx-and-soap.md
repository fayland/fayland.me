---
layout: post
title: "SSL pfx and SOAP"
description: ""
category: Perl
tags: ['SOAP', 'Perl', 'SSL']
---
{% include JB/setup %}

Sometimes you got a pfx file (with password pharse) that you can import it into Firefox certificates to view the website.

in Perl, it's a bit different, you first need use *openssl* to convert it into cert pem files.

	openssl pkcs12 -in test.pfx -out mycert.pem -nodes
	openssl rsa -in mycert.pem -out mycertkey.pem

with that, you got two files. then with LWP::UserAgent or any other modules based on it:

	my $ua = LWP::UserAgent->new(
		ssl_opts => {
			SSL_use_cert => 1,
		    verify_hostname => 0,
		    SSL_cert_file => "$Bin/mycert.pem",
		    SSL_key_file => "$Bin/mycertkey.pem",
		}
	)
	my $res = $ua->get("https://blabla.com/");

you can always use below to debug SSL:

	use IO::Socket::SSL qw(debug4);

and if the pfx is for SOAP::Lite, you can use something like below:

	$soap->transport->ssl_opts(
	    SSL_use_cert => 1,
	    verify_hostname => 0,
	    SSL_cert_file => "$Bin/mycert.pem",
	    SSL_key_file => "$Bin/mycertkey.pem",
	);

basically *transport* is LWP::UserAgent based on http(s) SOAP url.

Have fun.
