---
layout: page
title: Capitains
tagline: A tool suite for the CTS Norm
---

<img src="{{ BASE_PATH }}/assets/images/logo.png" width="200px"/>

## Internal documentation 

<ul>
{% assign pages_list = site.pages %}
{% assign group = 'navigation' %}
{% include JB/pages_list %}
</ul>

## External documentations

- [Capitains Sparrow (Javascript abstraction for CTS) API Documentation](http://capitains.github.io/Sparrow)
- [Capitains MyCapytain (Python Abstraction for CTS) Documentation](http://mycapytain.readthedocs.org/)

##Blogs :

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


<footer class="footer">
<img src="http://perseids.org/perseids_banner31.png" width="200px"/> <img src="/assets/images/perseus.png" width="200px"/> <img src="http://www.dh.uni-leipzig.de/wo/wp-content/uploads/2014/03/logo_dh_wid-300x57.png" width="200px"/><br />
Work on this tool suite has been funded by the [Humboldt Chair of the Digital Humanities at Leipzig](http://www.dh.uni-leipzig.de/wo/) and the [Andrew W. Mellon Foundation](http://www.mellon.org/).
</footer>