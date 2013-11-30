---
layout: post
title: "Email::Sender::Transport::SMTPS"
description: ""
category: "perl"
tags: ['perl', 'CPAN', 'Email', 'TLS']
---
{% include JB/setup %}

I just got a new CPAN module released: [Email::Sender::Transport::SMTPS](https://metacpan.org/pod/Email::Sender::Transport::SMTPS)

it's a replacement for [Email::Sender::Transport::SMTP::TLS](https://metacpan.org/pod/Email::Sender::Transport::SMTP::TLS).

the new module uses great [Net::SMTPS](https://metacpan.org/pod/Net::SMTPS) instead of a little messy [Net::SMTP::TLS::ButMaintained](https://metacpan.org/pod/Net::SMTP::TLS::ButMaintained)

here is few examples from the POD:

{% highlight perl %}
my $transport = Email::Sender::Transport::SMTPS->new({
  host => 'smtp.gmail.com',
  ssl  => 'starttls',
  sasl_username => 'myaccount@gmail.com',
  sasl_password => 'mypassword',
});
{% endhighlight %}

{% highlight perl %}
my $transport = Email::Sender::Transport::SMTPS->new(
  host => 'smtp.mandrillapp.com',
  ssl  => 'starttls',
  sasl_username => 'myaccount@blabla.com',
  sasl_password => 'api_key',
  helo => 'fayland.me',
);
{% endhighlight %}

{% highlight perl %}
my $transport = Email::Sender::Transport::SMTPS->new(
  host => 'email-smtp.us-east-1.amazonaws.com',
  ssl  => 'starttls',
  sasl_username => 'xx',
  sasl_password => 'zzz',
);
{% endhighlight %}

and you're welcome to give it a try and provide feedback!

Enjoy.