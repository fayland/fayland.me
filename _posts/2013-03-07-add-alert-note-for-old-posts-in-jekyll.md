---
layout: post
title: "add alert note for old posts in Jekyll"
description: ""
category: note
tags: ['Jekyll']
---
{% include JB/setup %}

## add alert note for old posts

For Jekyll Bootstrap, it's quite simple as we can do something like below:

edit *\_includes/themes/twitter/post.html*, add
{% raw %}
    {% assign page_year = page.date | date: "%Y" %}
    {% if page_year < '2010' %}
    <div class='alert alert-info'>This post may be outdated due to it was written on {{ page_year }}. The links may be broken. The code may be not working anymore. Leave comments if needed.</div>
    {% endif %}
{% endraw %}

## 20 items in rss/atom
I have another if in the {% raw %}{% for post in site.posts %}{% endraw %} for rss.xml and atom.xml

{% raw %}
    {% if forloop.index < 20 %}
    ...
    {% endif %}
{% endraw %}

## paginate

edit *\_config.yml*

    paginate: 10
    paginate_path: 'page/:num'

Have fun.