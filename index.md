---
layout: page
title: 首页
tagline: 
---

<ul class="posts">
  {% for post in site.posts %}
    <li>
      <span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
      <div class="indexContentContainer">{{ post.content }}</div>
    </li>
  {% endfor %}
</ul>