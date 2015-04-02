---
layout: page
title: Archive
permalink: /list/
---
<div class="container">
  <div id="article">
  <ul class="posts">
    {% for post in site.posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
</div>
