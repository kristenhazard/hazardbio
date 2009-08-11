---
layout: default
title: ksrr

section: ksrr
---
##Kristen's Science Reading Room
I've always wanted one of my own Christian Science Reading Rooms.  I don't know much about Christian Scientists, 
but I always thought it was super cool that they had their own reading rooms. So here is mine. It will take the 
form of a blog where I'll share all the things I'm interested in.  I'll also flesh out some ideas about a virtual 
Kristen's Science Reading Room I'm working on using the technology I'm building for [timesarrow](http://times-arrow.com).

<div id="blogtop">
  {% for post in site.categories.ksrr %}
  <div id="blogcontent">
  <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
    {{ post.content }}
    <h4>Posted on <a href="{{ post.url }}" title="Permalink for this post">{{ post.date | date_to_string }}</a></h4>
  </div>
  
  {% endfor %}
</div>



