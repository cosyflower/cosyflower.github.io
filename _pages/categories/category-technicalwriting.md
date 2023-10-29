---
title: "Technical Writing"
layout: archive
permalink: /categories/technicalwriting # permalink 항상 유의하기 
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.technicalwriting %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}