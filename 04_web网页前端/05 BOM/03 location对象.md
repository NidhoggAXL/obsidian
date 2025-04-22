# 一、location对象常见的属性

location对象用于表示window上当前链接到的URL信息。

常见的属性有哪些呢?

* **href**: 当前window对应的超链接URL, 整个URL;
* **protocol**: 当前的协议;
* **host**: 主机地址;
* **hostname**: 主机地址(不带端口);
* **port**: 端口;
* **pathname**: 路径;
* **search**: 查询字符串;
* **hash**: 哈希值;
* username:URL中的username(很多浏览器已经禁用)
* password:URL中的password(很多浏览器已经禁用)

# 二、location对象常见的方法
我们会发现location其实是URL的一个抽象实现:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1729172429000o0j6bc.png)

location有如下常用的方法:

* assign:赋值一个新的URL，并且跳转到该URL中;
* replace:打开一个新的URL，并且跳转到该URL中(不同的是不会在浏览记录中留下之前的记录)
* reload:重新加载页面，可以传入一个Boolean类型:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1734177400000kh3gwt.png)

# 三、URLSearchParams
URLSearchParams 定义了一些实用的方法来处理 URL的**查询字符串（片段）**。

* 可以将一个字符串转化成URLSearchParams类型;
* 也可以将一个URLSearchParams类型转成字符串

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17291728780003cv69j.png)


> 查询字符串
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17291728200008razga.png)

URLSearchParams常见的方法有如下:

* get:获取搜索参数的值;
* set:设置一个搜索参数和值,
* append:追加一个搜索参数和值;
* has:判断是否有某个搜索参数;
* https://developer.mozilla.org/zh-CN/docs/Web/AP//URLSearchParams

中文会使用**encodeURlComponent**和**decodeURlcomponent**进行编码和解码



