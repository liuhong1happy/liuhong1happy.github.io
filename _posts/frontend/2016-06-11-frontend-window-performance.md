---
layout: post
category : frontend
title: "window.performance相关文章"
tagline: "浏览器性能测试"
tags : [frontend,test]
theme :
  name : twitter
---
{% include JB/setup %}

=====原文链接=====

- [使用window.performance进行浏览器性能测试](http://www.wtoutiao.com/p/S47Kcn.html)
- [初探performance.timing API](http://www.th7.cn/web/html-css/201311/14802.shtml)

=========================================================================

# 使用window.performance进行浏览器性能测试

![window.performance](/assets/images/frontend/window.performance.jpg)

性能测试，其重要性不言而喻，以往前端的性能测试是非常不方便的，非常幸运的是现在有了一个新的api:window.performance，并且现在很多浏览器都支持了这个借口，这极大的降低了前端性能测试的难度。

## 一、理解浏览器的加载顺序

![window.performance](/assets/images/frontend/window.performance2.jpg)

从上图就可以知道浏览器加载顺序是如何的了，然后window.perference.timing就是提供了很多属性读取浏览器加载顺序上各个点的时刻(非时间，用专业的物理概念)，利用各个时刻的差值就可以得到我们想要的各加载段的时间。
不过，在chrome下，这里有一个坑，按照W3C的标准，navigationStart应该是整个过程的开始，也就是时间点应该最早。但是chrome下很多时候不是这样，会有domainLookupStart时间早于navigationStart的情况，初步认为应该是chrome的各种优化机制和预渲染功能打乱了上图的顺序。IE9相对守规矩一点。
window.perference.timing下的公开属性有：navigationStar、unloadEventStart、unloadEventEnd、redirectStart、redirectEnd、fetchStart、domainLookupStart、domainLookupEnd、connectStart、connectEnd、secureConnectionStart、secureConnectionStart、responseStart、responseEnd、domLoading、domInteractive、domContentLoadedEventStart、domContentLoadedEventEnd、domComplete、loadEventStart、loadEventEnd。与浏览器的加载顺序对于的点请对照上图。

## 二、浏览器的支持情况

IE：IE9以上支持，接口为window.msPerformance；
Chrome:chrome6以上支持，chrome6-9为window.webkitPerformance，chrome10中是window.performance；
Firfox：firfox7.0以上支持，接口为：window.msPerformance；
Safari:支持，接口为window.performance；
移动端：支持，接口为window.webkitPerformance。

## 三、timing.js

timing.js是github上一个对window.perfermence很好封装的一个开源js文件。

github地址：[https://github.com/addyosmani/timing.js](https://github.com/addyosmani/timing.js)

# 初探performance.timing API

浏览器新提供的performance接口精确的告诉我们当访问一个网站页面时当前网页每个处理阶段的精确时间(timestamp)，以方便我们进行前端分析。
它是浏览器的直接实现，比之前在网页中用js设置Date.time或者cookie来分析网页时间上要精确很多。
以下是w3c提供的performance.timing各阶段api图


![window.performance](/assets/images/frontend/window.performance2.jpg)

## 暂时的缺点：
 
Navigation Timing stops at the window.onload event
现代的网站很多是在onload之后再发触发更多的异步请求，而navigation Timing统计却只在window.onload之后就不统计了 。
为什么不在所有的网络请求完成后统计timing呢？
因为要考虑到有些网页有轮询或者长链接的情况。所以情况就复杂了，w3c还在草案阶段。如果你够牛想出好的解决方案，也可以直接发邮件到w3c去，贡献你的一份力量。

##  为方便查看统计值，自己写了一个简单的统计表插件

**performanceTracer**

performance API 耗时统计

统计点：

    readyStart = timing.fetchStart - timing.navigationStart;
    redirectTime = timing.redirectEnd  - timing.redirectStart;
    appcacheTime = timing.domainLookupStart  - timing.fetchStart;
    unloadEventTime = timing.unloadEventEnd - timing.unloadEventStart;
    lookupDomainTime = timing.domainLookupEnd - timing.domainLookupStart;
    connectTime = timing.connectEnd - timing.connectStart;
    requestTime = timing.responseEnd - timing.requestStart;
    initDomTreeTime = timing.domInteractive - timing.responseEnd;
    domReadyTime = timing.domComplete - timing.domInteractive; 
    //过早获取时 domComplete有时会是0
    loadEventTime = timing.loadEventEnd - timing.loadEventStart;
    loadTime = timing.loadEventEnd - timing.navigationStart;
    //过早获取时 loadEventEnd有时会是0

结果：

    console.log('准备新页面时间耗时: ' + readyStart);
    console.log('redirect 重定向耗时: ' + redirectTime);
    console.log('Appcache 耗时: ' + appcacheTime);
    console.log('unload 前文档耗时: ' + unloadEventTime);
    console.log('DNS 查询耗时: ' + lookupDomainTime);
    console.log('TCP连接耗时: ' + connectTime);
    console.log('request请求耗时: ' + requestTime);
    console.log('请求完毕至DOM加载: ' + initDomTreeTime);
    console.log('解释dom树耗时: ' + domReadyTime);
    console.log('load事件耗时: ' + loadEventTime);
    console.log('从开始至load总耗时: ' + loadTime);
    
使用方法：

可以直接在html底部引入performance-min.js
或下载chrome 插件.crx包，
 
注意事项

由于window.performance.timing还处于w3c完善过程中，当你的网站有异步请求时，请在所有异步请求完成后再点击chrome上的插件按钮，以确保数据正确
 
效果图：

![window.performance](/assets/images/frontend/99fc6033ab104bfdb58e7d517733ac46.png)

=======================================================================

js及chrome插件下载地址

github: [https://github.com/willian12345/performanceTracer](https://github.com/willian12345/performanceTracer)
 
关于performance timing 未完善功能老外的讨论：

[http://www.stevesouders.com/blog/2012/10/30/qa-nav-timing-and-post-onload-requests/](http://www.stevesouders.com/blog/2012/10/30/qa-nav-timing-and-post-onload-requests/)

==========================

转载处请注明：博客园偷饭猫willian12345@126.com