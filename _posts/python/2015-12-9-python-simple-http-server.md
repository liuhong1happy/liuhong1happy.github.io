---
layout: post
category : python
title: "python简单的HTTP Server"
tagline: "SimpleHTTPServer"
tags : [python]
---
{% include JB/setup %}

python自带了一个web服务器SimpleHTTPServer。我们可以很简单地输入下面的命令来启动web服务器，提供一个文件浏览的web服务。

    python -m SimpleHTTPServer 80

然后在浏览器输入`http://localhost`

就可以看到当前目录下的所有目录和文件了。

更复杂的用法直接可以看python的文档：[`http://docs.python.org/library/simplehttpserver.html`](http://docs.python.org/library/simplehttpserver.html)。
