---
title: "Web"
layout: archive
permalink: categories/frontend/web
author_profile: true
sidebar_main: true
---


{% assign posts = site.categories.Web %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
