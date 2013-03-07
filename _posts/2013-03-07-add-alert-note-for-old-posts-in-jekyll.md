---
layout: post
title: "add alert note for old posts in Jekyll"
description: ""
category: note
tags: ['Jekyll']
---
{% include JB/setup %}

For Jekyll Bootstrap, it's quite simple as we can do something like below:

edit *\_includes/themes/twitter/post.html*, add
{% raw %}
    {% assign page_year = page.date | date: "%Y" %}
    {% if page_year < '2010' %}
    <div class='alert alert-info'>This post may be outdated due to it was written on {{ page_year }}. The links may be broken. The code may be not working anymore. Leave comments if needed.</div>
    {% endif %}
{% endraw %}

another tip is that I just want 20 items in rss/atom, so I have another if in the {% raw %}{% for post in site.posts %}{% endraw %}

{% raw %}
    {% if forloop.index < 20 %}
    ...
    {% endif %}
{% endraw %}

Have fun.