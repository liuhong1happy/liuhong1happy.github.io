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
```js
function binarySearch(arry, val) {
	var start = 0
	var end = arry.length - 1
	while(start <= end) {
		let mid = (start + end) / 2;
		if(val > array[mid]) {
			start = mid + 1;
		} else if(val < array[mid]) {
			end = mid - 1;
		} else {
			return mid;
		}	
	}
	return -1;
}
```

10. http 协议

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

24. 常见的web前端性能优化的方法总结:

    性能优化主要包括DOM、网络的优化

    - DOM的优化 - 原则是减少DOM获取和渲染的频率，合理利用浏览器有限的资源，防止页面假死

        1. 少用全局变量、缓存DOM节点查找的结果。减少IO读取操作
        2. 用innerHTML代替DOM操作,减少DOM操作次数,优化javascript性能;
        3. 当需要设置的样式很多时,设置className而不是直接操作style
        4. 最大化浏览器性能，使用Web Worker来利用Web的多线程，防止主线程假死
        5. 优化数据结构， Redux 采用Immutale这种不可变对象，来对数据结构优化，减少过多的render
        6. 需要定时做某件事情的时候，使用requestAnimationFrame

    - 网络优化 - 减少请求数，压缩传输文件大小，预先加载，按需加载

        1. 减少http请求次数:CSS Sprites,JS、CSS源码压缩,控制图片大小;网页启用Gzip压缩,CDN托管,data缓存,图片服务器。
        2. 图片预加载,将样式表放在顶部,将脚本放置与底部加上时间戳
        3. 前端模板JS+数据,减少由于HTML标签导致的带宽浪费,前端使用变量保存ajax请求结果,每次操作本地变量,减少请求次数

25. requestAnimationFrame的特点

    requestAnimationFrame会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成，并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率

    在隐藏或不可见的元素中，requestAnimationFrame将不会进行重绘或回流，这当然就意味着更少的CPU、GPU和内存使用量

    requestAnimationFrame是由浏览器专门为动画提供的API，在运行时浏览器会自动优化方法的调用，并且如果页面不是激活状态下的话，动画会自动暂停，有效节省了CPU开销

26. 页面假死的原因

    页面大致分为 JS线程 GUI Render线程，事件触发线程。JS线程执行DOM操作本身比较耗时，这个过程会挂起GUI Render线程和事件触发线程，所以这个时候用户点击鼠标，敲打键盘都没有反应。

    等待JS线程执行完成后，需要更新一次GUI Render线程，才接着响应下一帧的事件或者setTimeout执行函数
    
27. CSS3 常用样式总结

    圆角(border-radius)、阴影（box-shadow）、位移(translate)和动画(transition、animation)
    文本（阴影text-shadow、折行word-wrap）、字体(@font-face)

28. 匹配连续两个相同字母或者数字

    `/([0-9a-zA-Z])\1+/`

    `[0-9a-zA-Z]` 匹配到字母或者数字
    `()` 会匹配到分组
    `\1` 表示上一个匹配到的分组
    `+` 表示一个以上的字符

29. js的基本数据类型有哪些？

    ECMAScript中有5中简单数据类型（也称为基本数据类型）: Undefined、Null、Boolean、Number和String。还有1中复杂的数据类型————Object，Object本质上是由一组无序的名值对组成的。

    其中Undefined、Null、Boolean、Number都属于基本类型。Object、Array和Function则属于引用类型，String有些特殊。

30. 区分数组Array和对象Object的几种方法？

    Array.prototype.isPrototypeOf(obj) //true表示是数组，false不是数组
    
    obj instanceof Array

    Array.isArray(obj);

    Object.prototype.toString.call(array)

    obj.constructor == Array

31. Electron main和render线程之间通信的方法

    1. ipc模式 main和render线程事件监听和调用
        ipcMain.on(channel, listener)
        ipcRenderer.on(channel, listener)
        ipcRenderer.send(channel, arg)
    2. remote
    3. webContents.executeJavaScript
32. RN 首屏渲染
33. css选择器优先级

    内联样式>id选择器>类和伪类选择器>元素选择器

34. React.PureComponent和React高阶组件
35. 懒加载的原理和实现

    定义：用户滚到特定位置才加载。
    原理：利用滚动事件以及getBoundingClientRect
    实现：滚动事件实时获取位置，比较getBoundingClientRect获取的位置信息进行比较
    
36. AMD、CMD和Common.js区别

37. Curring函数

    ```js
    var Curring = function(fn) {
        var args = [];
        return function() {
            if(arguments.length===0) {
                return fn.apply(this, args)
            }
            [].push.apply(args, arguments)
            return arguments.callee;
        }
    }
    var sum = function() {
        var result = 0;
        for(var i=0;i<arguments.length;i++) {
            result += arguments[i];
        }
        return result;
    }
    ```

38. setTimeout、setInterval、requestAnimationFrame代码先后执行顺序
    ```js
    requestAnimationFrame(function(){ 
        console.log("requestAnimationFrame");
    })
    var intervalInt = setInterval(function(){ 
        console.log("setInterval");
        clearInterval(intervalInt);
    });
    setTimeout(function(){ console.log("setTimeout") }); 
    ```


39. React Diff算法以及React setState发生的一系列过程

40. this是怎么什么时候被绑定的

41. 怎么理解vue的双向绑定，如果是你你会怎么实现？

42. 深拷贝与浅拷贝，以及vue是怎么避免深拷贝的？

    浅拷贝：1. for in语句 2. Object.assign
    深拷贝：
    1. 递归拷贝
    ```js
    function deepClone(initalObj, finalObj) {    
        var obj = finalObj || {};    
        for (var i in initalObj) {        
            if (typeof initalObj[i] === 'object') {
                obj[i] = (initalObj[i].constructor === Array) ? [] : {};            
                arguments.callee(initalObj[i], obj[i]);
            } else {
                obj[i] = initalObj[i];
            }
        }    
        return obj;
    }
    var str = {};
    var obj = { a: {a: "hello", b: 21} };
    deepClone(obj, str);
    console.log(str.a);
    ```
    2. Object.create() // 说白了是利用原型链


43. 原型、构造函数和实例之间的关系

    ```js
    var obj = {}; // 创建一个对象
    obj.__proto__ === Object.prototype // 实例和原型
    obj.__proto__.constructor === Object // 构造函数
    ```
    
    注意：

        1. 函数定义的时候，就已经创建了原型prototype,其中构造函数constructor指向了函数本身。
        2. new操作符，首先创建一个新的对象，将构造函数的作用域（this）赋给新的对象，然后执行构造函数，返回对象。

44. 继承

    原理一：原型链
    ```js
    var Animal = function(){}
    Animal.prototype.move = function(){
        console.log("move")
    } 
    var Dog = function(){}
    Dog.prototype = new Animal(); // 子类原型指向父类的实例
    var dog = new Dog();
    dog.move();
    ```
    原理二：借用构造函数
    ```js
    var Animal = function() {
        this.move = function() {
            console.log("move")
        } // 注意，这里必须在构造函数中定义变量和方法，不能复用函数
    }
    var Dog = function() {
        Animal.call(this); // 通过子类构造函数中调用父类构造函数（重新指向了this）
    }
    var dog = new Dog();
    dog.move();
    ```
    方法一：组合继承
    ```js
    var Animal = function() {
        this.name = "Animal"
    }
    Animal.prototype.sayName = function() { console.log(this.name)}
    var Dog = function() {
        Animal.call(this);  // 借用构造函数
    }
    Dog.prototype = new Animal(); // 原型链指向父类
    Dog.prototype.constructor = Dog; // 构造函数指向子类
    ``` 
    原理三：原型式继承(浅拷贝)
    ```js
    function object(o) {
        function F();
        F.prototype = o;
        return new F();
    }
    var obj = { foo: 1, bar : 2 }
    var cloneObj = object(o); // 以上等价于 var cloneObj = Object.create(obj);
    console.log(cloneObj.foo)
    ```
    原理四：寄生式继承
    ```js
    function createProperty(o) {
        var clone = object(o);
        clone.printFoo = function() {
            console.log(this.foo);
        }
        return clone;
    }
    var newObj = createProperty(obj);
    newObj.printFoo();
    ```
    方法二：寄生组合式继承
    ```js
    function inheritPrototype(Dog, Animal) {
        var prototype = Object(Animal.prototype); // 父类prototype先做一次拷贝
        prototype.constructor = Dog;
        Dog.protoype = prototype;
    }

    var Animal = function() {
        this.name = "Animal"
    }
    Animal.prototype.sayName = function() { console.log(this.name)}
    var Dog = function() {
        Animal.call(this);  // 借用构造函数
    }
    inheritPrototype(Dog, Animal);
    var dog = new Dog();
    dog.sayName();
    ```

45. Object.assign和Object.create内部实现

    ```js
    Object.prototype.assign = function (target) { 
        for (var i = 1; i < arguments.length; i++) { 
            var source = arguments[i]; 
            for (var key in source) { 
                if (Object.prototype.hasOwnProperty.call(source, key)) { 
                    target[key] = source[key]; 
                } 
            } 
        } 
        return target; 
    };
    Object.prototype.create = function(o) {
        function F() {};
        F.prototype = o;
        return new F();
    }
    ```

46. 怎么判断一个变量是undefined或者null

        target == null // 记住这里是两个等号

47. 斐波拉契数

    ```js
    var Fabonacci = function(n) {
        if(n===1 || n===2) return 1;
        return arguments.callee(n-1) + arguments.callee(n-2);
    }
    ```

48. 排序

    插入排序
    ```js 
    var array = [112, 33, 21, 90, 1, -20, 78];
    for(var i=1;i<array.length;i++) {
        for(var j=i;j>0 && array[j-1]>=array[j];j--) {
            var tmp = array[j-1];
            array[j-1] = array[j];
            array[j] = tmp;
        }
    }
    console.log(array);
    ```
    冒泡排序
    ```js 
    var array = [112, 33, 21, 90, 1, -20, 78];
    for(var i=0;i<array.length-1;i++) {
        for(var j=1;j<array.length-i;j++) {
            if(array[j]<array[j-1]) {
                var tmp = array[j-1];
                array[j-1] = array[j];
                array[j] = tmp;
            }
        }
    }
    console.log(array);
    ```
    快速排序
    ```js
    var array = [112, 33, 21, 90, 1, -20, 78];
    var quickSort = function(array, left, right) {
       if(left<right) {
           var baseIndex = division(array, left, right); // 找到基准值的中间位置
           quickSort(array, left, baseIndex-1); // 基准值左边的数继续排序
           quickSort(array, baseIndex+1, right); // 基准值右边的数继续排序
       }
    }
    var division = function(array, left, right) {
        let base = array[left];
        while(left<right) {
            while(base<=array[right] && left<right) right--; // 右边找到第一个比基准值小的数
            array[left] = array[right]; // 让其和最左边的数交换
            while(base>=array[left] && left<right) left++; // 左边继续找到第一个比基准值大的数
            array[right] = array[left]; // 让其和最右边的数交换
        }
        array[left] = base; // left和right相等的时候，就表示找到了基准值的位置
        return left; // 将基准值的下标返回
    }
    quickSort(array, 0, array.length-1);
    console.log(array);
    ```
    二分查找
    ```js
    var binarySearch = function(array, searchValue) {
        var low = 0;
        var high = array.length -1;
        while(low<high) {
            var n_2 = Math.floor((high+low)/2, 10);
            var base = array[n_2];
            if(base===searchValue) return n_2;
            else if(base<searchValue) low = n_2;
            else high = n_2;
        }
        return -1;
    }
    var findIndex = binarySearch([1,2,3,4,5,6,9,12,22,33,44,55], 44);
    console.log(findIndex);
    ```

49. 将普通数值，格式化为金钱格式

    ```js
    var val='212312.235423'
    var rex = /\d{1,3}(?=(\d{3})+$)/g;
    val.replace(/^(-?)(\d+)((\.\d+)?)$/, function (s, s1, s2, s3) {
         return '$' + s1 + s2.replace(rex, '$&,') + s3;
         // '$' + s1 + s2.replace(/\B(?=(?:\d{3})+(?!\d))/g,",")+ s3;
    })
    ```

50. 正则表达式中?=和?:和?!的理解

    要理解?=和?!，首先需要理解前瞻，后顾，负前瞻，负后顾四个概念：

        前瞻：
        exp1(?=exp2) 查找exp2前面的exp1
        后顾：
        (?<=exp2)exp1 查找exp2后面的exp1
        负前瞻：
        exp1(?!exp2) 查找后面不是exp2的exp1
        负后顾：
        (?<!=exp2)exp1 查找前面不是exp2的exp1
    
    举例：

        "中国人".replace(/(?<=中国)人/, "rr") // 匹配中国人中的人，将其替换为rr，结果为 中国rr
        "法国人".replace(/(?<=中国)人/, "rr") // 结果为 法国人，因为人前面不是中国，所以无法匹配到

    要理解?:则需要理解捕获分组和非捕获分组的概念：

        ()表示捕获分组，()会把每个分组里的匹配的值保存起来，使用$n(n是一个数字，表示第n个捕获组的内容)
        (?:)表示非捕获分组，和捕获分组唯一的区别在于，非捕获分组匹配的值不会保存起来

    举例：

        // 数字格式化 1,123,000
        "1234567890".replace(/\B(?=(?:\d{3})+(?!\d))/g,",") // 结果：1,234,567,890，匹配的是后面是3*n个数字的非单词边界(\B)

51. JavaScript 的正则表达式中的 \b 以及 \B 问题？

52. 实现一个Watcher类
    ```js
    class Watcher {
        constructor(data) {
            // your code
            const that = this;
            for(let key in data) {
                (function(data, key, value){
                    Object.defineProperty(that, key, {
                        configurable: true,
                        enumerable: true,
                        get: () => that._data[key],
                        set: (newValue) => {
                            if(that._data[key]!==newValue) {
                                that.$emit(key, newValue)
                            }
                        }
                    })
                })(data, key , data[key])
            }
            this._subs = {};
            this._data = data;
        }

        $on() {
            //your code
            let key = arguments[0];
            let callback = arguments[1];
            if(!this._subs[key]) this._subs[key] = [];
            this._subs[key].push(callback);
        }
        $emit() {
            // your code
            let key = arguments[0];
            let value = arguments[1];
            this._data[key] = value;
            if(!this._subs[key]) return;
            this._subs[key].forEach(callback=>{
                callback(value)
            })
        }
    }

    const w = new Watcher({a: 1});
    w.$on('a', (v) => {
        console.log('first ', v)
    })

    w.$on('a', (v) => {
        console.log('second ', v)
    })

    w.a = 2; // console: first 2  second 2

    w.$emit('a', 3); // console: first 3  second 3
    w.a === 3; // true
    ```
