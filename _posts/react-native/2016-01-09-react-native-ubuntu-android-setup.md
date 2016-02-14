---
layout: post
category : react-native
title: "基于ReactNative在Ubuntu 14.04环境快速开始Android应用开发"
tagline: "快速开始RN"
tags : [react,react-native,ubuntun,android]
theme :
  name : twitter
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


