Selenium 是 thoughtworks公司的一个集成测试的强大工具。最近参与了一个系统移植的项目，正好用到这个工具，把一些使用心得分享给大家，希望大家能多多使用这样的强大的，免费的工具，来保证我们的质量。

Selenium 的文档现存的不少，不过都太简单了。使用Selenium的时候，我更多的是直接去看API文档，好在API不错，一个一个看，就能找到所需要的 :-)   官方网站：http://www.openqa.org/selenium/

好，下面进入正题！

## 一、Selenium 的版本

`Selenium` 现在存在2个版本，一个叫 selenium-core, 一个叫selenium-rc 。

`selenium-core` 是使用HTML的方式来编写测试脚本，你也可以使用 `Selenium-IDE`来录制脚本，但是目前`Selenium-IDE`只有 FireFox 版本。

`Selenium-RC` 是 `selenium-remote control` 缩写，是使用具体的语言来编写测试类。

`selenium-rc` 支持的语言非常多，这里我们着重关注java的方式。这里讲的也主要是 selenium-rc，因为个人还是喜欢这种方式 :-)

## 二、一些准备工作

1、当然是下载 selenium 了，到 [http://www.openqa.org/selenium/](http://www.openqa.org/selenium/) 下载就可以了，记得选择selenium-rc 的版本。

2、学习一下 xpath 的知识。有个教程：[http://www.zvon.org/xxl/XPathTutorial/General_chi/examples.html](http://www.zvon.org/xxl/XPathTutorial/General_chi/examples.html)

一定要学习这个，不然你根本看不懂下面的内容！

3、安装 jdk1.5

## 三、selenium-rc 一些使用方法

在 selenium-remote-control-0.9.0\server 目录里，我们运行 java -jar selenium-server.jar。

之后你就会看到一些启动信息。要使用 selenium-rc ，启动这个server 是必须的。

当然，启动的时候有许多参数，这些用法可以在网站里看看教程，不过不加参数也已经足够了。

selenium server 启动完毕了，那么我们就可以开始编写测试类了！

我们先有个概念，selenium 是模仿浏览器的行为的，当你运行测试类的时候，你就会发现selenium 会打开一个浏览器，然后浏览器执行你的操作。

好吧，首先生成我们的测试类：

{% highlight java %}
public class TestPage2 extends TestCase {  
      private Selenium selenium;  
     
      protected void setUp() throws Exception {  
         String url = “http://xxx.xxx.xxx.xxx/yyy”;  
         selenium = new DefaultSelenium("localhost", SeleniumServer.getDefaultPort  
                                    (), "*iexplore", url);  
         selenium.start();            
         super.setUp();                       
     }  
     protected void tearDown() throws Exception {  
         selenium.stop();  
         super.tearDown();  
     }  
    
} 
{% endhighlight %}
　　代码十分简单，作用就是初始化一个 Selenium 对象。其中：

　　url : 就是你要测试的网站

　　localhost:  可以不是localhost，但是必须是 selenium server 启动的地址

　　*iexplore :  可以是其它浏览器类型，可以在网站上看都支持哪些。

　　下面我就要讲讲怎么使用selenium 这个对象来进行测试。