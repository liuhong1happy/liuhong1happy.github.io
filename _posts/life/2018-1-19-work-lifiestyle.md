---
layout: post
category : life
title: "工作的哪些事儿"
tagline: "解剖工作的奥秘"
tags : [life]
theme :
  name : twitter
---
{% include JB/setup %}

## 第一部分 面试

面试是工作的开始，所以先从面试开始，面试呐则需要熟悉面试时常见的问题。

我是一名前端工程师，当然这里我就只列出前端面试需要的一些面试题。

1. Webpack打包原理

    第一步：从入口文件开始递归地建立一个依赖关系图

    第二步：把所有文件都转化为模块函数

    第三步：根据配置文件，将模块函数打包到若干个bundle

    第四步：通过script标签把打包的bundle注入到html中，通过manifest文件来管理bundle文件的运行和加载。

    注：相关概念

        Entry 入口文件

        Output 怎么处理打包的代码

        Hot Module Replacement 热模块替换

        Tree Shaking 去除无用代码

        Code Splitting 代码拆分

        Lazy Loading 懒加载或者按需加载

        Loaders 把文件转换为模块

        The Manifest manifest文件用来引导所有模块的交互


2. Node相关：说明require的过程等

    第一步：解析path，如果有缓存就从缓存中读取，没有则按路径解析规则

        1、先从缓存中读取，如果没有则继续往下
        2、判断需要模块路径是否以/结尾，如果不是，则要判断
            a. 检查是否是一个文件，如果是，则转换为真实路径
            b. 否则如果是一个目录，则调用tryPackage方法读取该目录下的package.json文件，把里面的main属性设置为filename
            c. 如果没有读到路径上的文件，则通过tryExtensions尝试在该路径后依次加上.js，.json和.node后缀，判断是否存在，若存在则返回加上后缀后的路径
        3、如果依然不存在，则同样调用tryPackage方法读取该目录下的package.json文件，把里面的main属性设置为filename
        4、如果依然不存在，则尝试在该路径后依次加上index.js，index.json和index.node，判断是否存在，若存在则返回拼接后的路径。
        5、若解析成功，则把解析得到的文件名cache起来，下次require就不用再次解析了，否则若解析失败，则返回false

    第二步：解析成功后，加载文件

        js文件将在读入文件（同步读）内容后进行编译，json文件则用JSON.parse解析内容，node文件则使用dlopen进行动态链接库载入
        
        js文件在每个文件前后加上套，暴露require 、exports、module等对象


3. 如何技术选型

    1. 项目类型：后台、前台（纯展示、纯交互）
    2. 项目需求：兼容性要求是包括IE8、还是仅仅Chrome
    3. 团队成员状况：学习规划、工作热情
    4. 选择合适框架：可扩展性、兼容性、学习成本

4. 单页应用框架angular react vue
5. Js数组都有哪些方法及其作用、用法、返回值？详细说了一下splice()

    数组基础上修改：push pop shift unshift splice sort reverse copyWithin
    返回新的值：join map concat reduce indexOf find findIndex reduceRight some slice forEach

6. js数组去重有哪些办法
    1. 排序去重法
    2. indexOf去重法
    3. Object去重法
    4. Set去重法
7. 说明冒泡排序、插入排序实现的思想、步骤、每趟的结果等
    插入排序的思想：将数字插入到已排好序的队列中，直到所有数值排好序。
    冒泡排序的思想：队列中的数值两两比较，谁大放后面，一轮下来后最大的会被排在后面。
8. 什么是二分查找
9. http 协议

    Http报头分为通用报头，请求报头，响应报头和实体报头。 

    请求方的http报头结构：通用报头|请求报头|实体报头 

    响应方的http报头结构：通用报头|响应报头|实体报头

10. 正则表达式，匹配一个电话号码等

    这类问题，还是需要熟记正则表达式的相关规则

        1. []确定一类字符
        2. \d\w\s.表示一类字符
        3. ?+*{n,m} 确定字符个数
        4. ^$ 确定字符位置
        5. | 标示前后字符串选其一
        6. ()可以单独匹配项

    例如：

        1. 匹配电话号码

            /^((0\d{2,3}-\d{7,8})|(1[345789]\d{9}))$/

        2. 验证邮箱

            /^([a-zA-Z0-9\._-]+)@([a-zA-Z0-9_-]+)\.([a-zA-Z0-9_-]+)$/


11. margin重叠问题

    外边距重叠就是margin-collapse。

    在CSS当中，相邻的两个盒子（可能是兄弟关系也可能是祖先关系）的外边距可以结合成一个单独的外边距。这种合并外边距的方式被称为折叠，并且因而所结合成的外边距称为折叠外边距。

    折叠结果遵循下列计算规则：

    两个相邻的外边距都是正数时，折叠结果是它们两者之间较大的值。

    两个相邻的外边距都是负数时，折叠结果是两者绝对值的较大值。

    两个外边距一正一负时，折叠结果是两者的相加的和。

12. 说明一下盒模型

    content padding border margin ,长的像盒子

13. 如何设置一个元素不可见( 我说了3种方法，但是面试官说是4种╮(╯▽╰)╭ )

    高宽为0 // 高宽为0
    opacity为0 // 透明度为0
    display:none // 不可见
    position:fixed // 出界
    z-index:-1 // 堆栈布局底部

14. 说一下Vue的生命周期、特点，项目中为什么会选用vue而不用其他

15. 说明BFC及其使用

    相邻两个盒子之间的垂直的间距是被margin属性所决定的，在一个块级排版上下文中相邻的两个块级盒之间的垂直margin是折叠的

    BFC(Block Formatting Context)是Web页面中盒模型布局的CSS渲染模式。它的定位体系属于常规文档流。摘自W3C：浮动，绝对定位元素，inline-blocks, table-cells, table-captions,和overflow的值不为visible的元素，（除了这个值已经被传到了视口的时候）将创建一个新的块级格式化上下文。
    
    上面的引述几乎总结了一个BFC是怎样形成的。但是让我们以另一种方式来重新定义以便能更好的去理解。

    BFC有一下特性：

    内部的Box会在垂直方向，从顶部开始一个接一个地放置。

    Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生叠加

    每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。

    BFC的区域不会与float box叠加。

    BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之亦然。

    计算BFC的高度时，浮动元素也参与计算。

16. 简述ES6

    ES6狭义为ES2015，广义为下一代javascript。包含语法修改和类型或方法扩展。

    - 语法修改
        - let、const 块级作用域限定，防止变量提升，导致暂时性死区，不允许重复声明，const必须在声明时赋值。
        - 变量解构赋值 包括对象、数组、字符串、数字、布尔的解构赋值，undefined和null不能解构赋值
        - 模板字符串 \`123\`="123"
        - 标签模板 alert\`123\`=alert("123")
        - 函数扩展 参数解构、参数默认值、函数的 length 属性、参数作用域、rest 参数、函数的name属性、函数内部不能定义严格模式、尾调用优化
        - unicode表示方式 `\u{20BB7}`或者`\u0061`
        - 语调符号和重音符号的两种表示方式，比如 `O`（`\u004F`）和 `ˇ`（`\u030C`）合成 `Ǒ`（`\u004F\u030C`）
        - 迭代器Iterator与for of语句
        - 生成器Generator 
        - 装饰器
    - 类型的方法扩展
        - String方法扩展 `codePointAt`、`fromCodePoint`、`normalize`、`includes`、`startsWith`、`startsWith`、`repeat`、`padStart`、`padEnd`、`matchAll`、`raw`
        - RegExp扩展 `u`修饰符匹配unicode，`y`修饰符为“粘连”（sticky）修饰符，`s`修饰符，`.`可匹配所有字符，包括换行符。支持匹配`后行断言`、`\p\P`Unicode属性字符、具名组匹配及其引用`\k`
        - Number方法扩展 `isFinite`、`isNaN`、`isInteger`、`parseInt`、`parseFloat`、`isSafeInteger`
        - Math方法扩展 `trunc`、`sign`、`cbrt`、`clz32`、`imul`、`fround`、`hypot`、`expm1`、`log1p`、`log10`、`log2`、`sinh`、`cosh`、`tanh`、`asinh`、`acosh`、`atanh`
        - Array方法扩展 `from`、`of`、`copyWithin`、`fill`、`flat`、`flatMap`
        - Object方法扩展 `is`、`assign`、`getOwnPropertyDescriptors`、`setPrototypeOf`、`getPrototypeOf`、`fromEntries`、`getOwnPropertySymbols`
    - 数据类型、数据结构扩展
        - Symbol类型  
        - Set和Map类型 WeakSet和WeakMap防止内存释放
        - Proxy类型
        - Promise类型
        - ArrayBuffer类型
    - 运算符扩展
        - 指数运算符 `**`
        - 三点运算符 `...`
        - `::`绑定语法 代替bind、apply、call
        - 箭头函数 ()=>{} 不能new、没有arguments、内部不能使用yield、this指向的不是函数自身

17. 怎么理解ESLint
    - How？ ESLint配置主要由 解析器(parser)、解析器配置(parserOptions)、语法规则(rules)、运行环境(env)、全局变量(global)
    - What？ ESLint是对js语法规则进行校验得工具，默认为对ES5语法得校验。
    - Where? ESLint配置放置位置，主要有两种方式，一种是文件配置(例如.eslintrc.json、package.json)、一种是文件内注释配置(/* eslint-env node, mocha */)
    - When? ESLint需要在书写代码或者提交代码时进行代码语法检测。

18. 移动前端自适应适配布局解决方案

    方案：

        固定一个某些宽度，使用一个模式，加上少许的媒体查询方案
        使用flexbox解决方案
        使用百分比加媒体查询
        使用rem

19. bind、apply、call的区别

    bind是绑定函数的作用域this
    apply和call类似，是绑定作用域this然后执行，调用方式不通（`apply(thisObj,argArr)`和`call(thisObj,arg1,arg2,arg3,……)`）

20. 解释什么是柯里化函数

21. React Hooks

    React函数式组件，以前叫做`无状态组件`,只能接受props更改组件状态。现在React加入了钩子函数，改变`无状态组件`也能使用`state`和`setState`来实现内部状态管理，以及给`无状态组件`加入`componentDidMount`和`componentDidUpdate`等生命周期函数。

    ```jsx
    import { useState, useEffect } from 'react';

    function Example() {
        const [count, setCount] = useState(0);

        useEffect(() => {
            document.title = `You clicked ${count} times`;
        });

        return (
            <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>
                Click me
            </button>
            </div>
        );
    }
    ```

22. React Diff算法

首先，React采用虚拟dom来模拟虚拟的节点，这个虚拟节点比真实dom更加高效，不用一出生就带有很多标签。

整个diff算法，首先是对做了更改的节点进行标记，接着是同层级比较，新的元素将会新增，原有元素进行修改，不再有的元素标记回收。

比较原则当然是react分配的key值，或者我们手动设置的key值。

23. umi和dva、roadhog 是什么关系

roadhog 是基于 webpack 的封装工具，目的是简化 webpack 的配置

umi 可以简单地理解为 roadhog + 路由，思路类似 next.js/nuxt.js，辅以一套插件机制，目的是通过框架的方式简化 React 开发

dva 目前是纯粹的数据流，和 umi 以及 roadhog 之间并没有相互的依赖关系，可以分开使用也可以一起使用，个人觉得 umi + dva 是比较搭的