#  一、Web 网络字体
## 2.1 Web-fonts 的产生原因
**王之前我们有设置过页面使用的字体: font-family**

* 我们需要提供一个或多个字体种类名称，浏览器会在列表中搜寻，直到找到它所运行的系统上可用的字体
* 这样的方式完全没有问题，但是对于传统的web开发人员来说，字体选择是有限的;
* 这就是所谓的 **Web-safe 字体**;
* 并且这种默认可选的字体并不能进行一些定制化的需求;

比如下面的字体样式,系统的字体肯定是不能实现的

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723032120000pmgiyh.png)

那么我们是否依然可以在网页中使用这些字体呢?**使用Web Fonts即可**

**首先,我们需要通过一些渠道获取到希望使用的字体(不是开发来做的事情):**

* 对于某些**收费的字体**,我们需要获取到**对应的授权**;
* 对于某些**公司定制**的字体,需要**设计人员**来设计;
* 对于某些**免费的**字体,我们需要**获取到对应的字体文件**

**其次，在我们的CSS代码当中使用该字体(重要):**

* 具体的过程看后面的操作流程;

**最后,在部署静态资源时,将HTML/CSS/JavaScript/Font一起部署在静态服务器中;**

**用户的角度:**

* 浏览器一个网页时,因为代码中有引入字体文件, **字体文件会被一起下载下来**
* 浏览器会根据使用的字体在**下载的字体文件中査找、解析、使用对应的字体**
* **在浏览器中使用对应的字体显示内容**

## 2.2 web-fonts 的使用

**使用 Web Fonts：**

* 将字体放到对应的目录中
* 通过@font-face来引入字体,并且设置格式
* 使用字体

```css
<style>
	@font-face {
		font-family:"自己对引用的字体命名" ;
		src: url("引用的路劲");
	}
	div {
		font-family:"自己命名的字体" ;
	}
</style>
```

 > @font-face 用于加载一个自定义字体


## 2.3 web-fonts 的兼容性
**我们刚才使用的字体文件是.ttf，它是True Type字体。**

* 在开发中某些浏览器可能不支持该字体,所以为了浏览器的兼容性问题,我们需要有对应其他格式的字体;

**TrueType字体:拓展名是.ttf**

* OpenType/TrueType字体:拓展名是 .ttf、.otf建立在TrueType字体之上
* Embedded OpenType字体:拓展名是.eot,OpenType字体的压缩版
* SVG字体:拓展名是.svg、.svgz
* WOFF表示Web Open Font Format web开放字体拓展名是 .woff，建立在TrueType字体之上

> 这些做一些了解就可以啦，我们需要知道的是**大部分浏览器都支持 .ttf 、.otf 、.woff 的字体**就好。


**提供一个网站来生产对应的字体文件:**

* https://font.qqe2.com/# 暂时可用

**如果我们具备很强的兼容性，那么可以如下格式编写:**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17230862130006af1it.png)

更加标准的写法是在`{}`里面在添加上`font-style:; font-weight:;`

这被称为"bulletproof @font-face syntax(刀枪不入的@font-face语法)“:

* 这是 Paul lrish早期的一篇文章提及后@font-face开始流行起来(Bulletproof @font-face syntax)。

src用于指定字体资源

* url指定资源的路径
* format（格式）用于帮助浏览器快速识别字体的格式;

