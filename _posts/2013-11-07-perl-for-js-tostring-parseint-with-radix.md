---
layout: post
title: "Perl for JS toString parseInt with radix"
description: ""
category: "perl"
tags: ["perl", "javascript"]
---
{% include JB/setup %}

it's almost a copy-paste from module [JE](https://metacpan.org/release/JE). it's used in one of my code to parse JS code value with Perl.

{% highlight perl %}
sub js_toString {
    my ($num, $radix) = @_;

    return $num unless $radix;
    return $num if ($radix == 10 || $radix < 2 || $radix > 36 || $radix =~ /\./);

    if ($radix == 2) {
        return sprintf('%b', $num);
    } elsif($radix == 8) {
        return sprintf('%o', $num);
    } elsif($radix == 16) {
        return sprintf('%x', $num);
    }

    my $result = '';
    my @_digits = (0..9, 'a' .. 'z');
    while ($num >= 1) {
        substr($result,0,0) =
            $_digits[$num % $radix];
        $num /= $radix;
    }

    return $result;
}

sub js_parseInt {
    my ($str, $radix) = @_;

    return unless defined $str;
    $radix ||= 0;

    my $s = qr.[\p{Zs}\s\ck]*.;
    $str =~ s/^$s//;

    my $sign = $str =~ s/^([+-])//
        ? (-1,1)[$1 eq '+']
        :  1;
    $radix = (int $radix) % 2 ** 32;
    $radix -= 2**32 if $radix >= 2**31;
    $radix ||= $str =~ /^0x/i
    ?   16
    :   10
    ;
    $radix == 16 and
        $str =~ s/^0x//i;

    $radix < 2 || $radix > 36 and return;

    my @digits = (0..9, 'a'..'z')[0..$radix-1];
    my $digits = join '', @digits;
    $str =~ /^([$digits]*)/i;
    $str = $1;

    my $ret;
    if(! length $str){
        $ret = '';
    } elsif($radix == 10) {
        $ret = $sign * $str;
    } elsif($radix == 16) {
        $ret = $sign * hex $str;
    } elsif($radix == 8) {
        $ret = $sign * oct $str;
    } elsif($radix == 2) {
        $ret = $sign * eval "0b$str";
    } else {
        my ($num, $place);
        for (reverse split //, $str){
            $num += ($_ =~ /[0-9]/ ? $_
                : ord(uc) - 55)
                * $radix**$place++
        }
        $ret = $num*$sign;
    }

    return $ret;
}

say js_parseInt('z', 36); # 35
say js_toString(35, 36);  # 'z'

sub js_fromCharCode {
    my $str = '';
    my $num;
    for (@_) {
        # % 2**16 is buggy in perl
        $num = $_;
        $num = ($num < 0 ? ceil($num) : floor($num))
            % 2**16 ;
        $str .= chr($num == $num && $num);
            # change nan to 0
    }
    return $str;
}

sub js_charCodeAt {
    my ($str, $pos) = @_;

    if (defined $pos) {
        $pos = int($pos);
        $pos = 0 unless $pos == $pos;
    }

    return ($pos < 0 || $pos >= length $str)
            ? 0
            : ord substr $str, $pos, 1;
}

{% endhighlight %}