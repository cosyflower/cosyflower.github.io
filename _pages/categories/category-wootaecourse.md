---
title: "우아한테크코스"
layout: archive
permalink: /categories/wootaecourse
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.wootaecourse %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}