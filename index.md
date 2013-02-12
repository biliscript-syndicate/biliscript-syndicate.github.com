---
layout: page
title: 最近日志
tagline: 关于bilibili.tv弹幕播放器的技术文档和消息
---

<ul class="posts">
  {% for post in site.posts %}
    <li>
      <span>{{ post.date | date: "%Y年%m月%d日" }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
      <div class="indexContentContainer">{{ post.content }}</div>
    </li>
  {% endfor %}
</ul>
