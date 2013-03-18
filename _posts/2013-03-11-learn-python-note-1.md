---
layout: post
title: "Learn Python Note 1"
description: ""
category: python
tags: ['python']
---
{% include JB/setup %}

I'm starting learning Python a bit.

### argparse

if you have args setup in different modules, like you want setup `--log` on logging, setup `--tor` `--skip-tor` on requesting, the combination of *add_help=False* and *parse_known_args* is pretty cool.

    import argparse
    parent_argparse = argparse.ArgumentParser(add_help=False)
    parent_argparse.add_argument('--log', action='store', default='ERROR', dest='log', help='logging level: DEBUG, INFO, WARNING, ERROR, CRITICAL')
    _args, _args_unknown = parent_argparse.parse_known_args()

afterwards, in real place, do

    parser = argparse.ArgumentParser(description='Some real CLI', parents=[parent_argparse])

### __init__.py and as

actually it's a very cool feature. you can put some common code for all sub-modules in `__init__.py` like config code (to avoid write another file)

    import ConfigParser
    try:
        cfg = ConfigParser.ConfigParser()
        cfg.read(['/somwhere/conf/project.ini', '/somwhere/conf/project_local.ini'])
    except ConfigParser.Error, e:
        logger.critical('Cannot read configuration file, reason [%s]' % e)

and `as` is pretty amazing.

    from modulename import cfg as project_config

### BeautifulSoup is another HTML::TreeBuilder

BeautifulSoup works like Perl HTML::TreeBuilder.

    from bs4 import BeautifulSoup
    soup = BeautifulSoup(text)

    for tag in soup.find_all('span', attrs={'id': re.compile('^ctl00_contentPageContent_lbl(.*?)Value$')}):
        id = tag['id']
        id = id.replace('ctl00_contentPageContent_lbl', '').replace('Value', '')
        data[id] = tag.get_text()

### something I do like in Python

`def` with args and default values. (Perl `sub` was developed too many years ago.)

you don't need type so many `{}` or `()`.

### something I do not like in Python

string interpolation is quite inconvenience. there are `%`, `format` and Template. but I really miss the $ with Perl.

I miss Perl regexp a lot. the `re.compile`, `re.sub`, `re.I` is too much typing.

### Disclaim

I'm still a newbie. so parden me if anything is wrong. I'll write more when I learn more.  and I admit it's pretty fun to learn Python.

