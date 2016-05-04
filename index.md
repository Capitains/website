---
layout: page
title: CapiTainS
tagline: Tool suite and guidelines for CTS
logo: /assets/images/logo.png
---

[![DOI](https://zenodo.org/badge/doi/10.5281/zenodo.32701.svg)](http://dx.doi.org/10.5281/zenodo.32701)

CapiTainS is an informal open-source organization which aims at providing a suite of tools and guidelines for the CTS standards. Developers, guidelines contributor and more generally users are all welcome to join. You can contact us on github but more generally on [googlegroups](https://groups.google.com/forum/#!forum/capitains). You can find a few tutorials on our [youtube channel](https://www.youtube.com/channel/UCvwGuaIuATNfnM_TwhPMn7w). You can also contact individually the main maintainers of this repository on twitter : [Thibault Clérice](https://twitter.com/PonteIneptique) and [Bridget Almas](https://twitter.com/BridgetAlmas)

## Why you should browse and use our tools (and stay on this website longer)

- you have texts which you would like to make available as **digital editions**
- you care about people having access to your **open data**
- you want to **make linked open data a thing** without too much investment
- you want to **showcase your work** without too much development
- you want to **participate in a global effort of making data open and standard**
- as a **data consummer**, you want to **use CTS API** but you do not want to code everything yourself
- you are cool.

## Our (quite rare) blogs :

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## Pages you might be interested in 

<ul>
{% assign pages_list = site.pages %}
{% assign group = 'navigation' %}
{% include JB/pages_list %}
</ul>