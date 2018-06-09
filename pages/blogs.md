---
layout: page
title: "Blogs"
heahder: "Blogs"
group: navigation
description: ""
---
{% include JB/setup %}

We blog really rarely but maybe it will be of interest to you ! 

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>