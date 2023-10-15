---
title: "Bear To Blog"
layout: archive
permalink: /categories/beartoblog # permalink 항상 유의하기 
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.beartoblog %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}