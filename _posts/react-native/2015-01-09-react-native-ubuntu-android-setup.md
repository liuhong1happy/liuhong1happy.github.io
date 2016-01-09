---
layout: post
category : react-native
title: "基于ReactNative在Ubuntu 14.04环境快速开始Android应用开发"
tagline: "快速开始RN"
tags : [react,react-native,ubuntun,android]
---
{% include JB/setup %}

最近成功在Ubuntu 14.04上使用RN运行其简单的Demo，现将整个过程记录下来。

## 目录

- 准备工作
    - 安装git
    - 安装node和npm
    - 安装react-native-cli
    - 安装android sdk 并配置android avd
- 创建React Native Demo
    - 使用RNC创建示例工程代码
    - 安装NPM包
    - 运行android avd
    - 打包并传apk到AVD
    - 运行Dev Server
    - Reload JS并查看运行结果
    
## 准备工作

整个就绪工作，其实也不是很难，安装好相应开发环境需要的所有工具（这里就是Node、NPM、Git、react-native-cli和android sdk）。

#### 安装git

安装git相当的简单，一句命令就搞定。

        sudo apt-get install git-core
        
#### 安装node和npm

node需要是大于4版本，所以稍稍有点麻烦。

        apt-get install npm
        npm install -g n
        n 4.2.1
        npm install -g npm@3.3.3
        
如果安装成功，查看其版本

        node -v
        npm -v
        
#### 安装react-native-cli

安装好npm包管理工具，当然，安装react-native-cli也就很容易了。

        npm install -g react-native-cli
        
#### 安装android sdk 并配置android avd

安装Android SDK需要依赖JDK，所以务必先安装JDK。

        sudo apt-get install openjdk-7-jdk
        
**安装Android SDK**

官方下载页面，选择“USE AN EXISTING IDE”，下载不含IDE的纯SDK：官网 [http://developer.android.com/sdk/index.html](http://developer.android.com/sdk/index.html) ，国内镜像 [http://gmirror.org/#android-sdk-tools-only](http://gmirror.org/#android-sdk-tools-only)

        cd ~/Downloads/
        wget http://dl.gmirror.org/android/android-sdk_r24.4.1-linux.tgz
        tar -zxvf android-sdk_r24.4.1-linux.tgz
        echo 'export ANDROID_HOME="'$HOME'/Downloads/android-sdk-linux"' >> ~/.bashrc
        echo 'export PATH="$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools"' >> ~/.bashrc
        echo 'export JAVA_CMD="/usr/lib/jvm/java-7-openjdk-amd64/bin/java"' >> ~/.bashrc

**下载Android各版本的API**

    android

[这里](http://facebook.github.io/react-native/docs/android-setup.html#content)有详细的参考，需要安装哪些包。
    
![](/assets/images/react-native/AndroidSDK1.png)
![](/assets/images/react-native/AndroidSDK2.png)

**创建一个安卓虚拟设备**

运行如下命令，启动Android AVD面板。

    android avd

![](/assets/images/react-native/AndroidAVD.png)

Android AVD面板上单击`create`，开始创建安卓虚拟设备。

![](/assets/images/react-native/CreateAVD.png)

在Android AVD面板上选中刚才创建的安卓虚拟设备，并点击`start`就可以启动一个安卓虚拟设备。





## 创建React Native Demo

就绪工作做好了，我们就要开始直插要害的工作了，这里我们会用到react-native-cli。


#### 使用RNC创建示例工程代码

使用react-native-cli自动创建示例代码。

        react-native init TestReactNative
        
其目录结果如下

![](/assets/images/react-native/TestReactNative.png)

目录下有个文件叫做`index.android.js`，这就是整个RN工程的入口，待会儿详细讲解代码。

#### 安装NPM包

创建的示例代码中会有一个`package.json`文件，我们依据`package.json`文件运行npm install，安装所有的依赖包。

        npm install
    
#### 运行android avd

打开Android AVD面板

        android avd

启动刚才创建的安卓虚拟设备。

#### 打包并传apk到AVD

运行`react-native run-android`打包编译并传送apk到安卓虚拟设备。

#### 运行Dev Server

启动Dev Server

        react-native start

#### Reload JS并查看运行结果

回到安卓虚拟设备，单击`Reload JS`或者`F2选择Reload JS`。

这个时候就会看到我们整个项目运行的最终结果。




