---
layout: default
title: blog

section: blog
---

<span class="csr">create. share. repeat.</span>

<div id="blogtop">
  {% for post in site.categories.blog %}
  <div class="blogcontent">
    <span class="post-date">{{ post.date | date_to_string }}</span><br/>
    <a href="{{ post.url }}">{{ post.title }}</a>
    <p class="excerpt">{{ post.excerpt }}</p>
  </div>
  {% endfor %}
</div>

