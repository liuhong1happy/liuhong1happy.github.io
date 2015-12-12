---
layout: page
title: Liuhong's Blog
tagline: 人生到处知何似，应似飞鸿踏雪泥
---
{% include JB/setup %}


## 关于我

我是一名热爱前端的软件工程师,熟练使用`HTML5/CSS3`,熟练使用`Angularjs`和`Reactjs`.

![可爱的小女孩](/assets/images/liuhong1happy.jpg)

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

## 友情链接

#### 国内同行

- [阿里U一点](http://www.aliued.cn/)
- [新浪UED](http://ued.sina.com.cn/)
- [百度FEX](http://fex.baidu.com/)
- [腾讯网前端团队](http://qqfe.org/)
- [腾讯AlloyTeam](http://www.alloyteam.com/)
- [淘宝UED](http://ued.taobao.org/blog/)

#### 技术站点

- [ReactJS中文文档](http://reactjs.cn/)
- [ReactJS英文文档](https://facebook.github.io/react/)
- [Flux英文文档](http://facebook.github.io/flux/)



## 联系方式

- Email: [liuhong1.happy@163.com](mailto:liuhong1.happy@163.com)
- Weibo: [刚百](http://weibo.com/u/2186560121)
- Wechat: [jingxiyunjing](weixin://contacts/profile/jingxiyunjing)
- Github: [liuhong1happy](https://github.com/liuhong1happy)
- Telphone: [13648091632](callto://13648091632)
- QQ: [284362096](http://wpa.qq.com/msgrd?v=3&uin=284362096&site=qq&menu=yes)