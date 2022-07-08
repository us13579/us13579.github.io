---
title: "OS"
layout: archive
categories: OS
permalink: /category/OS/
author_profile: true
sidebar:
nav: "docs"
taxonomy: OS
---

{% assign posts = site.categories.OS %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
