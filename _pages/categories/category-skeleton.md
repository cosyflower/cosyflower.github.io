---
title: "Skeleton" # title 수정하는 것도 잊지 말기 
layout: archive
permalink: /categories/skeleton
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.skeleton %} <!-- categories.skeleton 변경해야 함 -->
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}