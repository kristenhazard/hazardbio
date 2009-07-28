---
layout: default
title: blog

section: blog
---



##create. share. repeat.

<div id="blogtop">
  {% for post in site.posts %}
  <div id="blogcontent">
  <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
    {{ post.content }}
    <h4>Posted on <a href="{{ post.url }}" title="Permalink for this post">{{ post.date | date_to_string }}</a></h4>
  </div>
  
  {% endfor %}
</div>



