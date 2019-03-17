---
layout: page
title: Liuhong's Blog
tagline: "人生到处知何似，应似飞鸿踏雪泥"
---
{% include JB/setup %}

## 关于我

我是一名热爱前端的软件工程师,熟练使用`HTML5/CSS3`,熟练使用`Angularjs`和`Reactjs`.

![可爱的小女孩](/assets/images/liuhong1happy.jpg)

## 文章列表

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date: "%Y年%-m月%-d日" }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## 标签列表

<ul class="tag_box inline">
  {% assign tags_list = site.tags %}  
  {% include JB/tags_list %}
</ul>

## 项目

- [E360Player](https://github.com/liuhong1happy/E360Player) 全景播放器
- [react-native-2048](https://github.com/ReactLover/react-native-2048) 2048小游戏

## 组件

- [similar-react-router](https://github.com/liuhong1happy/similar-react-router) 简单的路由
- [react-umeditor](https://github.com/liuhong1happy/react-umeditor) 富文本编辑器
- [react-raphael](https://github.com/liuhong1happy/react-raphael) raphael react化组件
- [react-native-wallpaper-manager](https://github.com/liuhong1happy/react-native-wallpaper-manager) 安卓壁纸

## 友情链接

#### 国内同行

| [阿里U一点](http://www.aliued.cn/) | [新浪UED](http://ued.sina.com.cn/) | [百度FEX](http://fex.baidu.com/) |
| :-------- | --------:| :------: |
| [腾讯网前端团队](http://qqfe.org/) | [腾讯AlloyTeam](http://www.alloyteam.com/) | [淘宝UED](http://ued.taobao.org/blog/) |

#### 前端技术站点

- [ECMAScript® 2016 Language Specification](http://www.ecma-international.org/ecma-262/7.0/index.html)
- [Bootstrap中文网](http://www.bootcss.com/)
- [ReactJS中文文档](http://reactjs.cn/)
- [ReactJS英文文档](https://facebook.github.io/react/)
- [React Redux英文文档](https://react-redux.js.org/introduction/quick-start)
- [Dva中文文档](https://dvajs.com/guide/)

#### 后端技术站点

- [Git中文文档](http://git-scm.com/book/zh/v2)
- [Beego官网](http://zh.beego.me/)
- [Docker官方英文文档](http://docs.docker.com)
- [Docker官方中文文档](http://dockerdocs.cn)
- [TensorFlow官方英文文档](http://tensorflow.org/)
- [TensorFlow官方中文](http://wiki.jikexueyuan.com/project/tensorflow-zh/)

#### 移动端技术站点

- [React Native英文文档](https://facebook.github.io/react-native/)
- [React Native中文文档](http://reactnative.cn/)
- [React Native官方网站](http://reactnative.com)

#### 桌面端技术站点

- [Qt 官网](http://www.qt.io/)
- [Electron 英文网址](http://electron.atom.io/)
- [Electron 中文文档](https://github.com/atom/electron/tree/master/docs-translations/zh-CN)
- [Electron 资源列表](https://github.com/sindresorhus/awesome-electron)
- [Electron 入门博文](https://www.sdk.cn/news/732)
- [CefSharp文档](https://github.com/cefsharp/CefSharp/wiki)

#### 测试技术站点

- [Selenium](http://www.51testing.com/zhuanti/selenium.html)
- [Puppeteer中文文档](https://zhaoqize.github.io/puppeteer-api-zh_CN/#/)

## 联系方式

- Email: [liuhong1.happy@163.com](mailto:liuhong1.happy@163.com)
- Weibo: [刚百](http://weibo.com/u/2186560121)
- Wechat: [jingxiyunjing](weixin://contacts/profile/jingxiyunjing)
- Github: [liuhong1happy](https://github.com/liuhong1happy)
- QQ: [284362096](http://wpa.qq.com/msgrd?v=3&uin=284362096&site=qq&menu=yes)
