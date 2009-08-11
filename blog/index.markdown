---
layout: default
title: blog

section: blog
---



##create. share. repeat.

<div id="blogtop">
  {% for post in site.categories.blog %}
  <div id="blogcontent">
    <span class="post-date">{{ post.date | date_to_string }}</span><br/>
    <a href="{{ post.url }}">{{ post.title }}</a>
    <p class="excerpt">{{ post.excerpt }}</p>
  </div>
  {% endfor %}
</div>



