# 一、什么jQuery
jQuery 读音为:/'d3ekwiari/(简称:jQ)，是一个快速、小型且功能丰富的 JavaScript 库，官网对jQuery的描述:

* 使HTML文档遍历、操作、事件具有易于使用的 API，可在多种浏览器中使用.
* 处理、动画和 Ajax 之类的事情变得更加简单。
* jQuery 结合多功能性和可扩展性，改变了数百万人编写 JavaScript 的方式。

jQuery官网:https://jquery.com/

兼容性：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17375388160007jatda.png)

> 基本不用考虑兼容的问题

# 二、库(library)和框架(framework)的概念
随着JavaScript的普及，以及越来越多人使用JavaScript来构建网站和应用程序

* JavaScript社区认识到代码中存在**非常多相同的逻辑**是可复用的。
* 因此社区就开始对这些**相同的逻辑的代码封装**到一个JavaScript文件中。
* 这个封装好的JavaScript文件就可称为**JavaScript库或JavaScript框架。**

库(library)

* JavaScript库是一个**预先编写好并实现了一些特定功能的代码片段的集合**
* 一个库中会包含许多的**函数、变量**等，可根据需求引入到项目中使用。
* 一些常见的库有jQuery、Day.js、Lodash和React等

框架(framework)

* JavaScript框架是一个**完整的工具集**，可帮助塑造和组织您的网站或应用程序。
* 提供一个结构来构建**整个应用程序**，，开发人员可以在结构的规则内**更安全、更高效**地工作。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/173754709500036k9ph.png)

比如：一个网站是使用Vue编写的，Vue里面有一些library，同时也可能会使用其他的library。


# 三、JQuery优点与缺点
jQuery的优点

* 易于学习:相对于其它的前端框架，jQuery 更易于学习，它支持 JavaScript 的编码风格。
* 少写多做(Write less, do more)
	* jQuery提供了**丰富的功能(DOM操作、过滤器、事件、动画、Ajax等)。**
	* 可以编写更少可读的代码来提高开发人员的工作效率。
* **优秀的 API 文档**:jQuery 提供了优秀的在线 API文档。
* 跨浏览器支持:提供出色的跨浏览器支持(IE9+)，无需编写额外代码

jQuery的缺点

* jQuery**代码库一直在增长**(自jQuery 1.5 起超过 200KB)
* 不支持**组件化**开发
* jQuery 更适合DOM操作，当涉及到**开发复杂的项目时，jQuery能力有限。**

原生代码：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17375476360008ws64m.png)

jQuery：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737547650000oj8r0z.png)

# 五、JQuery起源和历史
早在2005年8月22日, John Resig first hints of a JavaScript library to use csS selectors (Selectors in Javascript)with a moresuccinct syntax than existing libraries(Behaviour )

* John Resig 首次提出支持CSS选择器的JavaScript库，其语法比现有库(例如:Behaviour )更简洁。

在2006年之前，John Resig(一名从事自己项目的Web开发人员)对编写跨浏览器的JavaScript感到非常繁琐

* 2006年1月16日，John Resig在BarCamp的演讲中介绍了他的新库(jQuery)。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737548282000xouy8y.png)

之后John Resig又花了8个月的时间完善jQuery库，直到2006-8-26才发布了 1.0 版本。

* 原本打算使用JSelect(JavaScript Selectors)命名该库，但域名都已被占用。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737548304000ozzpju.png)


# 六、为什么学习jQuery
jQuery是一个非常受欢迎的JavaScript库，被全球约 7000 万个网站使用。它优秀的设计和架构思想非常值得我们去学习。

jQuery 的座右铭是“Write less,do more”，它易于学习， 非常适合JavaScript 开发人员学习的第一个库。

前端JavaScript库非常多，学习jQuery有利于我们学习和理解其它的JavaScript库(例如:Day.js、Lodash.js等)

许多大型科技公司，虽然他们现在不会直接使用jQuery来做项目，但在项目中仍然会借鉴很多jQuery设计思想。

因此，了解 jQuery 依然是一个好主意。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737548879000ck36ck.png)


# 七、jQuery的安装
jQuery 本质是一个**JavaScript 库**。

* 该库包含了:DOM操作、选择器、事件处理、动画和 Ajax 等核心功能。
* 现在我们可以简单的理解它就是一个JavaScript文件。
* 执行该文件中会给window对象添加一个jQuery函数(例如:window.jQuery)
* 接着我们就可以调用jQuery函数，或者使用该函数上的类方法。

下面我们来看看jQuery安装方式有哪些?

* 方式一:在页面中，直接通过CDN的方式引入。
* 方式二:下载jQuery的源文件，并在页面中手动引入。
* 方式三:使用npm包管理工具安装到项目中(npm在Node基础阶段会讲解)

## 7.1 认识CDN
什么是CDN呢?CDN称之为内容分发网络(Content Delivery Network或Content Distribution Network，缩写:CDN)

* CDN它是一组分布在不同地理位置的**服务器相互连接**形成的**网络系统**。
* 通过这个网络系统，将Web内容存放在**距离用户最近的服务器**
* 可以**更快、更可靠**地将Web内容(文件、图片、音乐、视频等)发送给用户,
* CDN不但可以提高资源的**访问速度**，还可以**分担源站的压力**。

更简单的理解CDN:

* CDN会**将资源缓存到遍布全球的网站**，用户请求获取资源时;
* 可**就近获取**CDN上缓存的资源，**提高资源访问速度，同时分担源站压力，**

常用的CDN服务可以大致分为两种:

* 自己购买的CDN服务:需要购买开通CDN服务(会分配一个域名)
	* 目前阿里、腾讯、亚马逊、Google等都可以购买CDN服务。
* 开源的CDN服务
	* 国际上使用比较多的是unpkg、JSDelivr、cdnjs、BootCDN等。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737549624000f1tbzm.png)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17375496280004sv8pp.png)


## 7.2 安装方式一： CDN
jQuery使用CDN方式引入

* `<script src="https://code.jquery.com/jquery-3.6.0.js"></script>`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17375515120001umb4n.png)

## 7.3 下载源码
下载jQuery的源码

* 官网下载:https://jquery.com/download/
* CDN连接地址下载:https://releases.jquery.com/jquery/
* GitHub仓库中下载:https://github.com/jquery/jquery

得到源码在通过js引入


# 八、jQuery初体验-计数器
原生js代码：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737555677000qwqmpi.png)

jQuery代码：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737556098000cb271q.png)

# 九、jQuery监听文档加载
jQuery监听document的[[07 常见事件#四、文档加载事件|DOMContentLoaded]]事件的四种方案

handler - 处理程序   deprecated - 弃用

* `$(document).ready(handler): deprecate-弃用`
* `$("document").ready(handler): deprecated-弃用`
* `$().ready(handler): deprecated-弃用`
* `$(handler)`:**推荐用这种写法，其它可以使用但是不推荐**

```js
<script src="../libs/jquery-3.6.0.js"></script>

<script>
 var $doc = $(document)
 $doc.ready(function() {
  console.log('doc ready')
 })
  
 jQuery('document').ready(function() {
  console.log('doc ready')
 })

 $().ready(function() {
  console.log('doc ready')
 })
  
 $(function() {
  console.log('doc ready')
 })
</script>
```

监听window的[[07 常见事件#四、文档加载事件|load]]事件，即网页所有资源(外部连接，图片等)加载完

* `.load(handler)`: This APl has been **removed in jQuery 3.0**
* `$(window).on('load',handler)`:推荐写法

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737558312000xqoqfo.png)

```js
<script>
 // $(window).load(function() {}) 3.0 remove

 $(window).on('load', function() {
  console.log('doc load')
 })
 
</script>
```


# 十、jQuery与其它库的变量名冲突
和 jQuery库一样，许多JavaScript库也会使用$作为函数名或变量名。

* 在 jQuery 中，**`$`是jQuery的别名,**
* 如果我们在使用jQuery库之前，其它库已经使用了`$`函数或者变量，这时就会出现冲突的情况。
* 这时我们可以通过调用jQuery中的**noConflict函数**来解决冲突问题。(conflict-冲突)
* jQuery在初始化前会**先备份**一下全局**其它库**的jQuery和`$`变量，调用noConfict函数只是**恢复**之前备份的jQuery和`$`变量。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737609258000vo01uc.png)

