---
layout: post
category : network
title: "OSX安装nginx和rtmp模块"
tagline: "视频流服务器搭建"
tags : [network,rtmp,nginx]
---
{% include JB/setup %}

参考文章:

  - [OSX安装nginx和rtmp模块（rtmp直播服务器搭建](http://www.cnblogs.com/damiao/p/5231221.html))
  

1. 安装Homebrew，执行命令

    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  
2. 执行命令：


    brew tap homebrew/nginx
    
3. 执行命令：

    brew install nginx-full --with-rtmp-module
    
  通过操作以上步骤nginx和rtmp模块就安装好了，下面开始来配置nginx的rtmp模块

  首先来看看我们的nginx安装在哪里了

    brew info nginx-full
    
 执行上面的命令后我们可以看到信息

    Docroot is: /usr/local/var/www
     
    The default port has been set in /usr/local/etc/nginx/nginx.conf to 8080 so that
    nginx can run without sudo.
     
    nginx will load all files in /usr/local/etc/nginx/servers/.
     
    - Tips -
    Run port 80:
     $ sudo chown root:wheel /usr/local/Cellar/nginx-full/1.8.1/bin/nginx
     $ sudo chmod u+s /usr/local/Cellar/nginx-full/1.8.1/bin/nginx
 
 
 nginx安装所在位置

    /usr/local/Cellar/nginx-full/
    
  nginx配置文件所在位置

    /usr/local/etc/nginx/nginx.conf
    
 nginx服务器根目录所在位置

    /usr/local/var/www
  
  执行命令 ，测试下是否能成功启动nginx服务

    /usr/local/Cellar/nginx-full/1.8.1/bin/nginx

 在浏览器地址栏输入：`http://localhost:8080`    如果出现

  **Welcome to nginx!**
  
代表nginx安装成功了

现在我们来修改nginx.conf这个配置文件，配置rtmp

4. 用记事本工具打开nginx.conf

    http {
        ……
    }
    // 在http节点后面加上rtmp配置：
    rtmp {
        server {
            listen 1935;
            application live1 {
                live on;
                record off;
            }
        }
    }

 然后保存文件后，重新加载nginx的配置文件

    /usr/local/Cellar/nginx-full/1.8.1/bin/nginx -s reload
 

  现在我们可以来对推流进行测试了 看看我们的rtmp能不能推流成功

  推流我们可以通过ffmepg来进行

5. 安装ffmepg工具

    brew install ffmpeg
    
 安装这个需要等一段时间等待吧 然后准备一个视频文件作为来推流，然后我们在安装一个支持rtmp协议的视频播放器，Mac下可以用VLC

  ffmepg 安装完成后可以开始推流了

6. 通过ffmepg命令进行推流

  ffmpeg -re -i /Users/Rick/Movies/Demo.mov -vcodec copy -f flv rtmp://localhost:1935/live1/room1

 这个room1是可以随便定义的，只要live1和上面nginx.conf里面配置的一样就行

  然后电脑上打开vlc这个播放器软件  点击File---->Open Network 在弹出来的框中选择Network然后输入URL:

    rtmp://localhost:1935/live1/room1

  这样就能看到通过ffmpeg推过来的视频了

  这就是一个简单的视频直播服务器的搭建
  
