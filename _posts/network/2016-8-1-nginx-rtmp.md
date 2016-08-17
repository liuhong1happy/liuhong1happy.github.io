---
layout: post
category : network
title: "OSX安装nginx和rtmp模块"
tagline: "视频流服务器搭建"
tags : [network,rtmp,nginx]
---
{% include JB/setup %}

0. 参考文章:

  - [OSX安装nginx和rtmp模块（rtmp直播服务器搭建](http://www.cnblogs.com/damiao/p/5231221.html))
  - [使用Nginx-rtmp-module搭建hls直播](http://www.xuebuyuan.com/2135082.html)
  
1. 安装Homebrew，执行命令

        ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  
2. 执行命令

        brew tap homebrew/nginx

3. 执行命令

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
                application rtmplive {
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
    
    安装这个需要等一段时间等待吧
    
    然后准备一个视频文件作为来推流，然后我们在安装一个支持rtmp协议的视频播放器，Mac下可以用VLC

    ffmepg 安装完成后可以开始推流了

6. 通过ffmepg命令进行推流

        ffmpeg -re -i /Users/liuhong/Movies/Demo.mov -vcodec copy -f flv rtmp://localhost:1935/rtmplive/home
        ffmpeg -re -i /Users/liuhong/Movies/Test.mp4 -vcodec libx264 -acodec aac -f flv rtmp://localhost:1935/rtmplive/home

    这个home是可以随便定义的，只要home和上面nginx.conf里面配置的一样就行

    然后电脑上打开vlc这个播放器软件  点击File---->Open Network 在弹出来的框中选择Network然后输入URL:

        rtmp://localhost:1935/rtmplive/home

    这样就能看到通过ffmpeg推过来的视频了

    这就是一个简单的视频直播服务器的搭建
  
7. http方式访问视频流

    HTTP Live Streaming（缩写是 HLS）是一个由苹果公司提出的基于HTTP的流媒体网络传输协议。是苹果公司QuickTime X和iPhone软件系统的一部分。它的工作原理是把整个流分成一个个小的基于HTTP的文件来下载，每次只下载一些。当媒体流正在播放时，客户端可以选择从许多不同的备用源中以不同的速率下载同样的资源，允许流媒体会话适应不同的数据速率。在开始一个流媒体会话时，客户端会下载一个包含元数据的extended M3U (m3u8) playlist文件，用于寻找可用的媒体流。

    HLS只请求基本的HTTP报文，与实时传输协议（RTP)不同，HLS可以穿过任何允许HTTP数据通过的防火墙或者代理服务器。它也很容易使用内容分发网络来传输媒体流。

    此协议详细内容请参考apple官方网站：[https://developer.apple.com/resources/http-streaming/](https://developer.apple.com/resources/http-streaming/)


    nginx-rtmp-module针对rtmp直播流实时转换为hls直播流的基本细节:`rtmp直播流会被动态切分为ts片段和一个不断刷新的u3m8文件`。

8. hls方式推流的nginx配置

        rtmp {
        
            server {
        
                listen 1935;
        
                chunk_size 4000;
              
                #HLS
        
                # For HLS to work please create a directory in tmpfs (/tmp/app here)
                # for the fragments. The directory contents is served via HTTP (see
                # http{} section in config)
                #
                # Incoming stream must be in H264/AAC. For iPhones use baseline H264
                # profile (see ffmpeg example).
                # This example creates RTMP stream from movie ready for HLS:
                #
                # ffmpeg -loglevel verbose -re -i movie.avi  -vcodec libx264 
                #    -vprofile baseline -acodec libmp3lame -ar 44100 -ac 1 
                #    -f flv rtmp://localhost:1935/hls/movie
                #
                # If you need to transcode live stream use 'exec' feature.
                #
                application hls {
                    live on;
                    hls on;
                    hls_path /usr/local/nginx/html/hls; # 对应下方root html;中html的路径。务必一致。
                    hls_fragment 5s;
                }
            }
        }
        
        http {
        
            server {
        
                listen  8080;
                location /hls {
                    # Serve HLS fragments
                    types {
                        application/vnd.apple.mpegurl m3u8;
                        video/mp2t ts;
                    }
                    root html; # 这里可以是指定目录
                    expires -1;
                }
            }
        }

8. 重启nginx服务

        /usr/local/Cellar/nginx-full/1.8.1/bin/nginx -s reload
        
9. ffmpeg推流

        ffmpeg -re -i /Users/liuhong/Movies/Test.mp4 -vcodec libx264 -acodec aac -f flv rtmp://localhost:1935/hls/home

10. 状态查看

    要查看到状态信息，需要在nginx.conf中加入stat模块的相关配置信息，也就是加入下面的几行信息，注意root的值是nginx-rtmp-module所在的目录

        location /stat {  
            rtmp_stat all;  
            rtmp_stat_stylesheet stat.xsl;  
        }  
        
        location /stat.xsl {  
            root /usr/local/src/nginx-rtmp-module/;  
        }

    注意为了得到统计信息，还需要开启下面的控制模块

        location /control {  
            rtmp_control all;  
        }  

    将它们添加到8080那台http虚机上的配置如下：

        rtmp {
        
            server {
        
                listen 1935;
        
                chunk_size 4000;
              
                #HLS
        
                # For HLS to work please create a directory in tmpfs (/tmp/app here)
                # for the fragments. The directory contents is served via HTTP (see
                # http{} section in config)
                #
                # Incoming stream must be in H264/AAC. For iPhones use baseline H264
                # profile (see ffmpeg example).
                # This example creates RTMP stream from movie ready for HLS:
                #
                # ffmpeg -loglevel verbose -re -i movie.avi  -vcodec libx264 
                #    -vprofile baseline -acodec libmp3lame -ar 44100 -ac 1 
                #    -f flv rtmp://localhost:1935/hls/movie
                #
                # If you need to transcode live stream use 'exec' feature.
                #
                application hls {
                    live on;
                    hls on;
                    hls_path /usr/local/nginx/html/hls;
                    hls_fragment 5s;
                }
            }
        }
        
        http {
        
            server {
        
                listen  8080;
        		
        		location /stat {  
        			rtmp_stat all;  
        			rtmp_stat_stylesheet stat.xsl;  
        		}  
        
        		location /stat.xsl {  
        			root /usr/local/src/nginx-rtmp-module/;  
        		}  
        		
        		location /control {  
        			rtmp_control all;  
        		}  
        
                location /hls {
                    # Serve HLS fragments
                    types {
                        application/vnd.apple.mpegurl m3u8;
                        video/mp2t ts;
                    }
                    root html;
                    expires -1;
                }
            }
        }
    然后，在浏览器中打开

        http://192.168.90.26:8080/stat
