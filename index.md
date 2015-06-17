---
layout: page
title: Capitains Organisation
tagline: A tool suite for the CTS Norm
---

## Collaborators

### Institutions
![Perseids](http://perseids.org/perseids_banner31.png)

![DH Leipzig](http://www.dh.uni-leipzig.de/wo/wp-content/uploads/2014/03/logo_dh_wid-300x57.png)

### Funders

Work on this tool suite has been funded by the [Humboldt Chair of the Digital Humanities at Leipzig](http://www.dh.uni-leipzig.de/wo/) and the [Andrew W. Mellon Foundation](http://www.mellon.org/).

##Blogs :

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


