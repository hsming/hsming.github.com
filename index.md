---
layout: page
title: Hsming
tagline:
---
{% include JB/setup %}



<ul class="posts">
  {% for post in site.posts %}
    <li>
      <h2><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h2>
      {{post.content}}
    </li>
  {% endfor %}
</ul>




