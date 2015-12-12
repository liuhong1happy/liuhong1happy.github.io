---
layout: page
title: 首页
tagline: 雕虫在此
---
{% include JB/setup %}

#### 关于我

我是lrongww，我是一名软件测试工程师，目前掌握的技术有： `Selemiun、java、TestNG` 测试框架等;

目前正处于学习技术的阶段，我要成为一名资深的测试工程师，请相信我！
    
#### 文章列表

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

#### 标签列表

<ul class="tag_box inline">
  {% assign tags_list = site.tags %}  
  {% include JB/tags_list %}
</ul>


#### 联系方式

Email: [373362292@qq.com](mailto:373362292@qq.com)
