---
layout: post
category : TestNG
title: "TestNG入门教程"
tagline: "TestNG的预备知识"
tags : [TestNG]
---
{% include JB/setup %}

国庆7天假期，大部分朋友都出去旅游了，微信圈里全是晒旅游的照片， 东南亚游，欧洲游呀，真是羡慕呀。 悲惨的我只去了上海野生动物园， 在家休息，利用这段假期，把之前学过的东西都总结下。 

我前段时间加班太多了，每天忙碌工作，都没精力去管自己的学习新技能的计划, 博客也没写几篇，很多想做的事情都因为工作太忙而耽搁了。 所以工作太忙了也不好，没有精力关注工作以外的事情。   

最近写自动化测试每天都用到TestNG,  把常用的TestNG的用法总结下。

## 阅读目录

1. TestNG介绍
2. 在Eclipse 中安装TestNG插件
3. TestNG最简单的测试
4. TestNG的基本注解
5. TestNG中如何执行测试
6. TestNG中按顺序执行Case
7. TestNG异常测试
8. TestNG组测试
9. TestNG参数化测试
10. TestNG忽略测试
11. TestNG 依赖测试
12. TestNG测试报告

## TestNG介绍

TestNG是Java中的一个测试框架， 类似于JUnit 和NUnit,   功能都差不多， 只是功能更加强大，使用也更方便

Java中已经有一个JUnit的测试框架了。  TestNG比JUnit功能强大的多。  测试人员一般用TestNG来写自动化测试。  开发人员一般用JUnit写单元测试。

官方网站: [http://testng.org/doc/index.html](http://testng.org/doc/index.html)

## 在Eclipse中安装TestNG

打开Eclipse   Help ->Install New Software ,   然后Add   "[http://beust.com/eclipse](http://beust.com/eclipse)"

![Install New Software](/assets/images/testng/030942544628581.png)

## TestNG最简单的测试

下面是TestNG的最简单的一个例子
 
{% highlight java %}
package TankLearn2.Learn;

import org.junit.AfterClass;
import org.junit.BeforeClass;
import org.testng.annotations.Test;

public class TestNGLearn1 {

    @BeforeClass
    public void beforeClass() {
        System.out.println("this is before class");
    }

    @Test
    public void TestNgLearn() {
        System.out.println("this is TestNG test case");
    }

    @AfterClass
    public void afterClass() {
        System.out.println("this is after class");
    }
}
{% endhighlight %}

## TestNG的基本注解

<table>
    <tr> <td>@BeforeSuite</td>	 <td>注解的方法将只运行一次，运行所有测试前此套件中。</td> </tr>
    <tr> <td>@AfterSuite</td>	 <td>注解的方法将只运行一次此套件中的所有测试都运行之后。</td> </tr>
    <tr> <td>@BeforeClass</td>	 <td>注解的方法将只运行一次先行先试在当前类中的方法调用。</td> </tr>
    <tr> <td>@AfterClass</td>	 <td>注解的方法将只运行一次后已经运行在当前类中的所有测试方法。</td> </tr>
    <tr> <td>@BeforeTest</td>	 <td><pre>注解的方法将被运行之前的任何测试方法属于内部类的 <test>标签的运行。</pre></td> </tr>
    <tr> <td>@AfterTest</td>	 <td><pre>注解的方法将被运行后，所有的测试方法，属于内部类的<test>标签的运行。</pre></td> </tr>
    <tr> <td>@BeforeGroups</td>	 <td>组的列表，这种配置方法将之前运行。此方法是保证在运行属于任何这些组第一个测试方法，该方法被调用。</td> </tr>
    <tr> <td>@AfterGroups</td>	 <td>组的名单，这种配置方法后，将运行。此方法是保证运行后不久，最后的测试方法，该方法属于任何这些组被调用。</td> </tr>
    <tr> <td>@BeforeMethod</td>	 <td>注解的方法将每个测试方法之前运行。</td> </tr>
    <tr><td> @AfterMethod </td><td>被注释的方法将被运行后，每个测试方法。 </td></tr>
	<tr><td> @DataProvider </td><td>标志着一个方法，提供数据的一个测试方法。注解的方法必须返回一个 Object[] []，其中每个对象[]的测试方法的参数列表中可以分配。
该@Test 方法，希望从这个DataProvider的接收数据，需要使用一个 dataProvider名称等于这个注解的名字。  </td></tr>
    <tr><td> @Factory </td><td>  作为一个工厂，返回TestNG的测试类的对象将被用于标记的方法。该方法必须返回 Object[]。</td></tr>
    <tr><td> @Listeners </td><td>定义一个测试类的监听器。  </td></tr>
    <tr><td> @Parameters </td><td> 介绍如何将参数传递给@Test方法。 </td></tr>
    <tr><td> @Test </td><td>标记一个类或方法作为测试的一部分。 </td></tr>
</table>
	
	
## TestNG中如何执行测试

第一种直接执行：右键要执行的方法，　　点Run As ->TestNG Test

![TestNG Test](/assets/images/testng/050727158475617.png)

第二种:  通过testng.xml文件来执行. 把要执行的case, 放入testng.xml文件中。 右键点击testng.xml,   点Run As

testng.xml

{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd" >
<suite name="Suite1">
    <test name="test12">
        <classes>
            <class name="TankLearn2.Learn.TestNGLearn1" />
        </classes>
    </test>
</suite>
{% endhighlight %}

![testng.xml](/assets/images/testng/050729215814295.png)

## TestNG按顺序执行Case

在testng.xml中，可以控制测试用例按顺序执行。  当preserve-order="true"是，可以保证节点下面的方法是按顺序执行的

{% highlight xml %}

<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd" >
<suite name="Suite1">
    <test name="test12" preserve-order="true">
        <classes>
            <class name="TankLearn2.Learn.TestNGLearn1">
                <methods>
                    <include name="TestNgLearn3" />
                    <include name="TestNgLearn1" />
                    <include name="TestNgLearn2" />
                </methods>
            </class>
        </classes>
    </test>
</suite>

{% endhighlight %}

## TestNG异常测试

测试中，有时候我们期望某些代码抛出异常。

TestNG通过@Test(expectedExceptions)  来判断期待的异常， 并且判断Error Message

{% highlight java %}
package TankLearn2.Learn;

import org.testng.annotations.Test;

public class ExceptionTest {
    
    @Test(expectedExceptions = IllegalArgumentException.class, expectedExceptionsMessageRegExp="NullPoint")
    public void testException(){
        throw new IllegalArgumentException("NullPoint");
    }
}
{% endhighlight %}

## TestNG组测试

TestNG中可以把测试用例分组，这样可以按组来执行测试用例比如：

{% highlight java %}
package TankLearn2.Learn;

import org.testng.annotations.Test;

public class GroupTest {
    
    @Test(groups = {"systemtest"})
    public void testLogin(){
        System.out.println("this is test login");
    }
    
    @Test(groups = {"functiontest"})
    public void testOpenPage(){
        System.out.println("this is test Open Page");
    }
}
{% endhighlight %}

然后在testng.xml中 按组执行测试用例

{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd" >
<suite name="Suite1">
    <test name="test1">
        <groups>
        <run>
        <include name="functiontest" />
        </run>
    </groups>
    </test>
</suite>
{% endhighlight %}


## TestNG参数化测试

软件测试中，经常需要测试大量的数据集。 测试代码的逻辑完全一样，只是测试的参数不一样。  这样我们就需要一种 “传递测试参数的机制”。 避免写重复的测试代码

TestNG提供了2种传递参数的方式。

第一种: testng.xml 方式使代码和测试数据分离，方便维护

第二种：@DataProvider能够提供比较复杂的参数。 (也叫data-driven testing)

 

方法一：　通过testng.xml 传递参数给测试代码

{% highlight java %}
package TankLearn2.Learn;

import org.testng.annotations.Parameters;
import org.testng.annotations.Test;

public class ParameterizedTest1 {
    
    @Test
    @Parameters("test1")
    public void ParaTest(String test1){
        System.out.println("This is " + test1);
    }
}
{% endhighlight %}

testng.xml

{% highlight xml %}

<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd" >
<suite name="Suite1">
        <parameter name="test1" value="Tank" />
        <parameter name="test1" value="Xiao" />
    <test name="test12">
        <classes>
            <class name="TankLearn2.Learn.ParameterizedTest1" />
        </classes>
    </test>
</suite>

{% endhighlight %}

方式二:   通过DataProvider传递参数

{% highlight java %}
package TankLearn2.Learn;

import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;

public class DataProviderLearn {
    
    @DataProvider(name="user")
    public Object[][] Users(){
        return new Object[][]{
                {"root","passowrd"},
                {"cnblogs.com", "tankxiao"},
                {"tank","xiao"}
        };
    }
    
    @Test(dataProvider="user")
    public void verifyUser(String userName, String password){
        System.out.println("Username: "+ userName + " Password: "+ password);
    }
}
{% endhighlight %}

## TestNG忽略测试

有时候测试用例还没准备好， 可以给测试用例加上@Test(enable = false)，  来禁用此测试用例

{% highlight java %}
package TankLearn2.Learn;

import org.testng.annotations.Test;

public class TesgNGIgnore {
    
    @Test(enabled = false)
    public void testIgnore(){
        System.out.println("This test case will ignore");
    }
}
{% endhighlight %}


## TestNG 依赖测试

{% highlight java %}
package TankLearn2.Learn;

import org.testng.annotations.Test;

public class DependsTest {
    
    @Test
    public void setupEnv(){
        System.out.println("this is setup Env");
    }
    
    @Test(dependsOnMethods = {"setupEnv"})
    public void testMessage(){
        System.out.println("this is test message");
    }
}
{% endhighlight %}

## TestNG测试结果报告

测试报告是测试非常重要的部分.  

TestNG默认情况下，会生产两种类型的测试报告HTML的和XML的。 测试报告位于 "test-output" 目录下.

![test-output](/assets/images/testng/050741002222302.png)

当然我们也可以设置测试报告的内容级别. 

verbose="2" 标识的就是记录的日志级别，共有0-10的级别，其中0表示无，10表示最详细

{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd" >
<suite name="Suite1">
    <test name="test12" verbose="2">
        <classes>
            <class name="TankLearn2.Learn.TestNGLearn1" />
        </classes>
    </test>
</suite>
{% endhighlight %}

