---
title: "WEB"
layout: archive
categories: WEB
permalink: /category/WEB/
author_profile: true
sidebar:
nav: "docs"
taxonomy: WEB
---

{% assign posts = site.categories.WEB %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
