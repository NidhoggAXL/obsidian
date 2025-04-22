# 一、认识Emmet
**Emmet(前身为 Zen Coding)是一个能大幅度提高前端开发效率的一个工具。**

* 在前端开发的过程中，一大部分的工作是写 HTML、CSS 代码,如果手动来编写效果会非常低
* VsCode内置了Emmet语法,在后缀为.html/.css中输入缩写后按Tab/Enter键即会自动生成相应代码

**!和html:5可以快速生成完整结构的htm15代码**


**`>`（子代）和 `+`（兄弟）**

```html
div>h1>span+h2
```
\
生成下面的 html 结构

```html
<div>

	<h1>

		<span></span>

		<h2></h2>

	</h1>

</div>
```

**`*`（多个） 和 `^`（上一级）**

**`（）`分组**

**属性`[id属性、class属性、普通属性]{}`(内容)**

**`$`（数字）**

```html
ul>li{列表属性$$$}*3
```

```html
<ul>

	<li>列表属性001</li>

	<li>列表属性002</li>

	<li>列表属性003</li>

</ul>
```

回进行自动的一个排序，有几个`$`符号就有几位数字进行排序。

**`.`隐式标签**

一般情况下面是 div

```html
.noe+.two
```

```html
<div class="noe"></div>

<div class="two"></div>
```

特殊情况下面也不一定是 div 元素。

```html
ul>.box{列表元素$}*3
```

```html
<ul>

	<li class="box">列表元素1</li>

	<li class="box">列表元素2</li>

	<li class="box">列表元素3</li>

</ul>
```

**CSS Emmet**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1722954440000qdzgmx.png)



