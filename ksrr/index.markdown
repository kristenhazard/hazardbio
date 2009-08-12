---
layout: default
title: ksrr

section: ksrr

---
##Kristen's Science Reading Room

I've always wanted one of my own Christian Science Reading Rooms.  I don't know much about Christian Scientists, 
but I always thought it was super cool that they had their own reading rooms. So here is mine. It will take the 
form of a blog where I'll share all the things I'm interested. Check out my [timesarrow](http://times-arrow.com) 
version of [Kristen's Science Reading Room](http://times-arrow.com/timelines/16) as well.

<div id="blogtop">
  {% for post in site.categories.ksrr %}
  <div id="blogcontent">
    <span class="post-date">{{ post.date | date_to_string }}</span><br/>
    <a href="{{ post.url }}">{{ post.title }}</a>
    <p class="excerpt">{{ post.excerpt }}</p>
  </div>
  {% endfor %}
</div>



