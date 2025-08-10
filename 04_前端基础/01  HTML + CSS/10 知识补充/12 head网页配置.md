# 一、meta

**meta元素用于定义元数据:**

* 在之前讲解head的时候说过，head中用于定义元数据
* 比如标题title、样式style、link外部资源等;
* meta用于定义那些不能使用其他定元相关(meta-related)元素定义的任何元数据信息;

**meta 元素定义的元数据的类型包括以下几种:**

* 如果设置了 charset 属性，**meta** 元素是一个字符集声明，告诉文档使用哪种字符编码。
* 如果设置了 **http-equiv** 属性，meta 元素则是编译指令,
	* 现在已经不用啦。
* 如果设置了 **name** 属性，meta 元素提供的是**文档级别**(document-level)的元数据，应用于整个页面。

官方文档：https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/meta

## 1.1 http-qquiv

我们会发现，无论是默认创建的html页面还是王者荣耀都有如下代码:

`<meta http-equiv="X-UA-Compatible" content="IE=edge">`

它的作用到底是什么呢?网上众说纷纭，我们直接看官方文档的解释

* 告知IE浏览器去模仿哪一个浏览器的行为,
* lE=edge，告知IE8区使用最高有效模式来模仿;



## 1.2 name 
name 的值非常多，具体内容查看文档：https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/meta/name

**几个常用的：**

* **robots**:爬虫、协作搜寻器，或者，对此页面的处理行为，或者说，应当遵守的规则。“机器人"
* **author**:文档作者的名字
* **Copyright**:版权声明;
* **description**:一段简短而精确的、对页面内容的描述,
	* 一些浏览器，比如 Firefox 和 Opera，将其用作书签的默认描述。
	* SEO优化
* **keywords**:与页面内容相关的关键词，使用逗号分隔。
	* 某些搜索引擎会进行收录;
	* SEO优化

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17261316220003of9wy.png)


# 二、link
Favicon是favoritesicon的缩写，亦被称为websiteicon(站点图标)、pageicon(页面图标);

```html
    <link rel="shortcut icon" href="favicon.ico" type="image/x-icon">
    <link rel="icon" href="">
```

上面那个是兼容 IE 浏览器的，不过现在也不在使用 IE 浏览器了。

为什么王者荣耀没有link元素也可以正常显示图标呢?

王者的代码另一个局限就是它把favicon关联到了某个特定的HTML或XHTML文档上。为避免这一点，favicon.ico文件应置于根目录下。多数浏览器将自动检测并使用它

> [!tip] 重点
> 在我们开发中还是尽量使用link来引入，而不是放到工程文件的根目录下面来使用。
> 最好的就是两种同时进行设置


下面的link使用方法表示有另一个可替换的网站供选择

```html
<link rel="alternate" href="https://pvp.gg.com/m/">`
```


# 三、CSS样式字符编码

之前我们有制定过HTML页面的编码，但是并没有制定CSS样式的编码，

* 那么CSS样式的字符编码会按照什么规则来使用呢?

**在样式表中有多种方法去声明字符编码，浏览器会按照以下顺序尝试下边的方法(一旦找到就停止并得出结果）：**

1. 文件的开头的 Unicode byte-order(字节顺序标记)字符值。
	* https://en.wikipedia.org/wiki/Byte_order_markV
1. 由Content-Type:HTTP header 中的 charset 属性给出的值或用于提供样式表的协议中的等效值。
2. CSS @规则 @charset.
3. 使用参考文档定义的字符编码:`<link>`元素的 charset 属性。
	* 该方法在 HTML5 标准中已废除，无法使用。
1. 假设文档是 UTF-8。

> [!tip] 开发建议
> 开发中推荐在CSS的开头编写@charset指定编码

