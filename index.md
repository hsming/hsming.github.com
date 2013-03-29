---
layout: page
title: Hsming
tagline:
---
{% include JB/setup %}




{% for post in site.posts limit:2 %}
  <div class="posts">
      <h2>
      	<a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
      	<span style="float:right">
      		{{ post.date | date_to_string }}
      	</span>
      </h2>
      <div class="article">
      	{{post.content}}
      </div>
  </div>
{% endfor %}


<h2><a href="/archive.html"> >>Read more.</a></h2>



