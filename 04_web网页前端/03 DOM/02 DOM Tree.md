# 一、DOM Tree的理解
一个页面不只是有html、head、body元素，也包括很多的子元素:

* 在html结构中，最终会形成一个树结构，
* 在抽象成DOM对象的时候，它们也会形成一个树结构，我们称之为DOM Tree:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1734090911000rykk5z.png)

# 二、DOM的继承关系图


DOM相当于是JavaScript和HTML、CSS之间的桥梁

* 通过浏览器提供给我们的**DOM API**，我们可以对元素以及其中的内容做任何事情;

类型之间有如下的继承关系：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1734090943000nk7mzl.png)

# 三、document对象

Document节点表示的整个载入的网页，它的实例是全局的document对象:

* 对DOM的所有操作都是从 document 对象开始的;
* 它是DOM的 **入口点**，可以从document开始去访问任何节点元素，

对于最顶层的html、head、body元素，我们可以直接在document对象中获取到:

* html元素:`<html>=document.documentElement`
* body元素:`<body>=document.body`
* head元素:`<head>=document.head`
* 文档声明:`<!DOCTYPE html>=document.doctype`


