---
layout: page
title: Hello World!
tagline: Supporting tagline
---
{% include JB/setup %}

## 关于我

我是新手，请多多关照！
    
## 文章列表

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## 标签列表

<ul class="tag_box inline">
  {% assign tags_list = site.tags %}  
  {% include JB/tags_list %}
</ul>


{% for tag in site.tags %} 
  <h2 id="{{ tag[0] }}-ref">{{ tag[0] }}</h2>
  <ul>
    {% assign pages_list = tag[1] %}  
    {% include JB/pages_list %}
  </ul>
{% endfor %}