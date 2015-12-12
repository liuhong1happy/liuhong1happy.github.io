---
layout: post
category : network
title: "应对DNS污染"
tagline: "添加固定IP到hosts"
tags : [network]
---
{% include JB/setup %}

这一段时间github老是挂掉，总是让人很烦。

无奈之举，自己手动添加github的真实IP到本地hosts配置文件中。

    192.30.252.129       github.com
    23.235.33.133        github.io
    185.31.18.133        liuhong1happy.github.io

当然，这些IP是需要提前ping的，打开终端。

    ping github.com

随后会返回主机IP和相应报文回应时间，当然我们这里考虑返回的主机IP。
