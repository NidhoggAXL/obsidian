# 一、认识DOM和BOM
前面我们花了很多时间学习JavaScript的基本语法，但是这些基本语法，但是这些语法好像和做网页没有什么关系，和前面学习的HTML、CSS也没有什么关系呢?

* 这是因为我们前面**学习的部分属于ECMAScript**，也就是**JavaScript本身的语法部分;**
* 除了语法部分之外，我们还需要**学习浏览器提供给我们开发者的DOM、BOM相关的API才能对页面、浏览器**进行操作

前面我们学习了一个window的全局对象，window上事实上就包含了这些内容:

* 我们已经学习了**JavaScript语法部分的Object、Array、Date**等;
* 另外还有**DOM、BOM部分**


DOM:文档对象模型(Document 0bject Model)

* 简称 DOM，将**页面所有的内容表示为可以修改的对象**

BOM:浏览器对象模型(Browser Object Model)

* 简称 BOM，由浏览器提供的用于**处理文档(document))之外的所有内容的其他对象:**
* 比如[[05 navigator、screen对象(很少使用)|navigator]]、[[03 location对象|location]]、[[04 history对象|history]]等对象;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1727952835000hc8t1b.png)


# 二、深入理解DOM
浏览器会对我们编写的HTML、CSS进行渲染，同时它又要考虑我们可能会通过JavaScript来对其进行操作:

* 于是浏览器将我们编写在HTML中的每一个元素(Element)都抽象成了一个个对象;
* 所有这些对象都可以通过JavaScript来对其进行访问，那么我们就可以通过JavaScript来操作页面，
* 所以，我们将这个抽象过程称之为 **文档对象模型(Document Object Model)**;

整个文档被抽象到 document 对象中:

* 比如document.documentElement对应的是html元素
* 比如document.body对应的是body元素
* 比如document.head对应的是head元素;

下面的一行代码可以让整个页面变成红色

```js
document.body.style.background = "red"
```



