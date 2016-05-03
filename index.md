---
layout: page
title: Capitains
tagline: A tool suite for the CTS Standard
logo: /assets/images/logo.png
---

## Citation

[![DOI](https://zenodo.org/badge/doi/10.5281/zenodo.32701.svg)](http://dx.doi.org/10.5281/zenodo.32701)

`Thibault Clérice et al.. (2015). Capitains Guidelines for CTS. Zenodo. 10.5281/zenodo.32701`

## Internal documentation 

<ul>
{% assign pages_list = site.pages %}
{% assign group = 'navigation' %}
{% include JB/pages_list %}
</ul>

## External documentations

- [Capitains Sparrow (Javascript abstraction for CTS) API Documentation](http://capitains.github.io/Sparrow)
- [Capitains MyCapytain (Python Abstraction for CTS) Documentation](http://mycapytain.readthedocs.org/)

## Blogs :

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>