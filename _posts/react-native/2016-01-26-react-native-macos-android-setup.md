---
layout: post
category : react-native
title: "基于ReactNative在Mac OS X环境快速开始Android应用开发"
tagline: "快速开始RN"
tags : [react,react-native,macosx,android]
theme :
  name : twitter
---
{% include JB/setup %}

最近成功在Mac OSX10上使用RN运行其简单的Demo，现将整个过程记录下来。

## 目录

- 准备工作
    - 安装brew
    - 安装npm和node
    - 安装react-native-cli
    - 安装JDK
    - 安装android sdk
    - 配置android avd
- 创建React Native Demo
    - 使用RNC创建示例工程代码
    - 安装NPM包
    - 运行android avd
    - 打包并传apk到AVD
    - 运行Dev Server
    - Reload JS并查看运行结果
- Demo代码研读
    - index.android.js文件中代码
    - Style与Flex布局
- 创建更加复杂的应用程序
    - Image
    - ListView
    - fetch
    - final
- 真机运行调试
    - 安装apk
    - 运行apk
    - 设置Dev Settings
    - Reload JS

## 准备工作

在Mac OSX系统中，准备工作中首先要安装brew，其次通过brew安装git、npm、node、jdk和android-sdk。

#### 安装brew

安装brew相对简单，使用如下命令：

    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

安装完成后，需要安装git并修改brew的镜像源地址。

    brew install git
    # 重新安装brew以达到更换镜像源地址的目的
    cd ~/tmp
    git clone git://mirrors.tuna.tsinghua.edu.cn/homebrew.git
    rm -rf /usr/local/.git
    rm -rf /usr/local/Library
    cp -R homebrew/.git /usr/local/
    cp -R homebrew/Library /usr/local/

## 安装npm和node

安装完brew，后续的工作都很简单了，例如安装npm和node

    # 这里安装npm就会顺带安装node
    brew install npm

更换npm镜像源

    # 编辑 ~/.npmrc 加入下面内容
    registry = https://registry.npm.taobao.org
    
## 安装react-native-cli

有了npm，一切js包都尽收囊中。

    npm install react-native-cli

## 安装JDK

下载[jdk](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)。点击安装即可！

![JavaJDK](/assets/images/react-native/JavaJDK.png)

## 安装android sdk

    # so easy
    brew install android-sdk
    # vim ~/.bashrc 写入如下内容：
    export ANDROID_HOME=/usr/local/opt/android-sdk

android sdk配置东软镜像源并安装应该安装的包

    android sdk

打开过后，系统界面最上边，Android SDK Manager -> Preferences...

![](/assets/images/react-native/AndroidSDKManager.png)

http proxy server这里填写： mirrors.neusoft.edu.cn

端口填写80，然后把Force https:// 前的勾勾上
    
mac顶部菜单Tools->Manage Add-on Site

![](/assets/images/react-native/AddOnSite.png)

把下面这堆网址：

    http://mirrors.neusoft.edu.cn/android/repository/addon-6.xml 
    http://mirrors.neusoft.edu.cn/android/repository/addon.xml 
    http://mirrors.neusoft.edu.cn/android/repository/extras/intel/addon.xml 
    http://mirrors.neusoft.edu.cn/android/repository/sys-img/android-tv/sys-img.xml 
    http://mirrors.neusoft.edu.cn/android/repository/sys-img/android-wear/sys-img.xml 
    http://mirrors.neusoft.edu.cn/android/repository/sys-img/android/sys-img.xml 
    http://mirrors.neusoft.edu.cn/android/repository/sys-img/google_apis/sys-img.xml 
    http://mirrors.neusoft.edu.cn/android/repository/sys-img/x86/addon-x86.xml 
    http://mirrors.neusoft.edu.cn/android/repository/addons_list-2.xml 
    http://mirrors.neusoft.edu.cn/android/repository/repository-10.xml

全手动New加进去，然后就可以下载了

注：上图中加圈的项，建议勾上，否则有可能创建不了Android模拟设备

## 配置android avd

**安装HAXM**

安装步骤参考如下

[Intel® Hardware Accelerated Execution Manager](https://software.intel.com/en-us/android/articles/intel-hardware-accelerated-execution-manager)

接着运行如下命令，启动Android AVD面板。

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

#### 运行Node Server

启动Node Server

    react-native start

#### Reload JS并查看运行结果

回到安卓虚拟设备，单击`Reload JS`或者`F2选择Reload JS`。

这个时候就会看到我们整个项目运行的最终结果。

![](/assets/images/react-native/WelcomeToReactNative.png)

## Demo代码研读

在安卓虚拟设备运行React Native Demo后，我们来看看项目中的代码结构。

#### index.android.js文件中代码

{% highlight js %}

'use strict';

var React = require('react-native');
var {
  AppRegistry,
  StyleSheet,
  Text,
  View,
} = React;

var TestReactNative = React.createClass({
  render: function() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>
          Welcome to React Native!
        </Text>
        <Text style={styles.instructions}>
          To get started, edit index.android.js
        </Text>
        <Text style={styles.instructions}>
          Shake or press menu button for dev menu
        </Text>
      </View>
    );
  }
});

var styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});

AppRegistry.registerComponent('TestReactNative', () => TestReactNative);

{% endhighlight %}

我们可以看出，其代码大致是这样的。

{% highlight js %}

var TestReactNative = React.createClass({
  render: function() {
    return (...);
  }
});

var styles = StyleSheet.create({...});

AppRegistry.registerComponent('TestReactNative', () => TestReactNative);

{% endhighlight %}

`React.createClass`创建了一个React组件类。

`StyleSheet.create`创建了一个供React组件类使用的样式，该样式类似js中的style。

`AppRegistry.registerComponent`为整个应用注册TestReactNative组件。



#### Style与Flex布局

我们学习React的相关知识，知道类似的写法。Web端React的style遵循CSS的样式写法，支持浏览器所兼容的样式，其Flex收到浏览器的兼容性限制，使用不是很多。

但是，对于移动端原生Native组件布局类似与Flex布局，所以React Native中原生支持Flex布局写法。

对于Flex布局，记住其是由Flex Box和Flex Item组成就行。

Flex Box规定所有Flex Item所遵循的排布方式（例如行列显示，垂直布局，水平布局等）。

Flex Item可以单独规定其内部样式以及在Flex Box中单独的布局样式。


## 创建更加复杂的应用程序

通过了解代码结构，这次我们就开始书写新的代码，以此了解React Native部分组件。

本次要创建的项目是电影列表，一张图片，标题和上演时间。

{% highlight js %}

var {
  AppRegistry,
  Image,
  StyleSheet,
  Text,
  View,
} = React;

var MOCKED_MOVIES_DATA = [
  {title: 'Title', year: '2015', posters: {thumbnail: 'http://i.imgur.com/UePbdph.jpg'}},
];

var TestReactNative = React.createClass({
  render: function() {
    var movie = MOCKED_MOVIES_DATA[0];
    return (
      <View style={styles.container}>
        <Text>{movie.title}</Text>
        <Text>{movie.year}</Text>
        <Image source={{uri: movie.posters.thumbnail}}  style={styles.thumbnail}/>
      </View>
    );
  }
});

var styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  thumbnail: {
    width: 53,
    height: 81,
  },
});

AppRegistry.registerComponent('TestReactNative', () => TestReactNative);

{% endhighlight %}

#### Image

首先，通过我们之前了解的View、Text等基本控件，加上Image，我们显示单个电影作品的详细信息。

这里，Image控件，需要除了传入style元素外，还需要传入图片的地址内容，即要设定`source`属性。当然，这类似与Web端的src属性。

#### ListView

当然，我们需要显示更多的数据，一条电影作品信息是远远不够的。

这里我们会接下来用到ListView。

{% highlight xml %}
<ListView dataSource={this.state.dataSource} renderRow={this.renderMovie} style={styles.listView} />
{% endhighlight %}

ListView由数据源dataSource和每一个Item的显示组件renderRow组成，style规定其样式。

其renderMoview：

{% highlight js %}

renderMovie: function(movie) {
    return (
      <View style={styles.container}>
        <Image
          source={{uri: movie.posters.thumbnail}}
          style={styles.thumbnail}
        />
        <View style={styles.rightContainer}>
          <Text style={styles.title}>{movie.title}</Text>
          <Text style={styles.year}>{movie.year}</Text>
        </View>
      </View>
    );
  },
{% endhighlight %}

#### fetch

当然，有了View还是需要数据滴，我们常常调取数据都是通过Web API的方式去调用。为了方便理解，这次我们采用直接调取远端JSON的方式，同时在组件创建完成过后加载数据。

{% highlight js %}

  componentDidMount: function() {
    this.fetchData();
  },
  fetchData: function() {
    fetch(REQUEST_URL)
      .then((response) => response.json())
      .then((responseData) => {
        this.setState({
          dataSource: this.state.dataSource.cloneWithRows(responseData.movies),
          loaded: true,
        });
      })
      .done();
  },
  
{% endhighlight %}


#### final

最终代码如下：

{% highlight js %}

'use strict';

var React = require('react-native');
var {
  AppRegistry,
  Image,
  ListView,
  StyleSheet,
  Text,
  View,
} = React;

var API_KEY = '7waqfqbprs7pajbz28mqf6vz';
var API_URL = 'http://api.rottentomatoes.com/api/public/v1.0/lists/movies/in_theaters.json';
var PAGE_SIZE = 25;
var PARAMS = '?apikey=' + API_KEY + '&page_limit=' + PAGE_SIZE;
var REQUEST_URL = API_URL + PARAMS;

var TestReactNative = React.createClass({
  getInitialState: function() {
    return {
      dataSource: new ListView.DataSource({
        rowHasChanged: (row1, row2) => row1 !== row2,
      }),
      loaded: false,
    };
  },

  componentDidMount: function() {
    this.fetchData();
  },

  fetchData: function() {
    fetch(REQUEST_URL)
      .then((response) => response.json())
      .then((responseData) => {
        this.setState({
          dataSource: this.state.dataSource.cloneWithRows(responseData.movies),
          loaded: true,
        });
      })
      .done();
  },

  render: function() {
    if (!this.state.loaded) {
      return this.renderLoadingView();
    }

    return (
      <ListView
        dataSource={this.state.dataSource}
        renderRow={this.renderMovie}
        style={styles.listView}
      />
    );
  },

  renderLoadingView: function() {
    return (
      <View style={styles.container}>
        <Text>
          Loading movies...
        </Text>
      </View>
    );
  },

  renderMovie: function(movie) {
    return (
      <View style={styles.container}>
        <Image
          source={{uri: movie.posters.thumbnail}}
          style={styles.thumbnail}
        />
        <View style={styles.rightContainer}>
          <Text style={styles.title}>{movie.title}</Text>
          <Text style={styles.year}>{movie.year}</Text>
        </View>
      </View>
    );
  },
});

var styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'row',
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  rightContainer: {
    flex: 1,
  },
  title: {
    fontSize: 20,
    marginBottom: 8,
    textAlign: 'center',
  },
  year: {
    textAlign: 'center',
  },
  thumbnail: {
    width: 53,
    height: 81,
  },
  listView: {
    paddingTop: 20,
    backgroundColor: '#F5FCFF',
  },
});

AppRegistry.registerComponent('TestReactNative', () => TestReactNative);

{% endhighlight %}

就类似与这样的方式，来组织


## 真机运行调试

如果我们不想安装虚拟机，想采用真机进行运行调试的话，将大大减少开启虚机的时间，也大大解决开发主机的内存消耗。

#### 安装apk

选择要实现真机运行调试的项目。进入项目路径，运行：

    react-native run-android
    
通过USB将手机解决电脑，启动USB调试功能，安装apk

    adb install android/app/build/outputs/apk/app-debug.apk
    
或者将apk拷入手机中并安装。

#### 运行apk

单击安装好的调试应用以运行应用。

运行Node Server。

#### 设置Dev Settings

按安卓手机最左边的那个按键（HOME键旁边）。

![](/assets/images/react-native/F2.png)

选择Dev Settings

![](/assets/images/react-native/DevSettings.png)

选择输入可供调试的server的IP和端口。

![](/assets/images/react-native/IP&Port.png)

点击确定。

返回应用。

#### Reload JS

仍然是单击左边的按键，选择Reload JS。

这是我们就可以看到运行后的结果。

