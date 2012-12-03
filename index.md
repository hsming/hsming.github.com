---
layout: page
title: Hsming
tagline:
---
{% include JB/setup %}



<ul class="posts">
  {% for post in site.posts %}
    <li>
      <h2>
      	<a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
      	<span style="float:right">
      		{{ post.date | date_to_string }}
      	</span>
      </h2>
      <div class="article">
      	{{post.content}}
      </div>
    </li>
    <h3>

    	<a href="{{ BASE_PATH }}{{ post.url }}">→Read On</a>
    </h3>
  
    <br />
  {% endfor %}
</ul>




