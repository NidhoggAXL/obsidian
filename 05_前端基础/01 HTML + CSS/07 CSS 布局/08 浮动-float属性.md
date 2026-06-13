# 一、认识浮动
**float 属性可以指定一个元素应沿其容器的左侧或右侧放置，允许文本和内联元素环绕它。**

* float 属性最初只用于在一段文本内浮动图像,实现文字环绕的效果;
* 但是早期的CSS标准中并没有提供好的左右布局方案,因此在一段时间里面它成为网页多列布局的最常用工具,

**绝对定位、浮动都会让元素脱离标准流，以达到灵活布局的效果**

**可以通过float属性让元素产生浮动效果，float的常用取值**

* none:不浮动，默认值
* left:向左浮动
* right:向右浮动

# 二、浮动的规则
## 2.1 规则一
**元素一旦浮动后,脱离标准流**

* 朝着向左或向右方向移动，直到**自己的边界紧贴着包含块**(一般是父元素)或者其他浮动元素的边界为止
* **定位元素会层叠在浮动元素上面**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723538766000ckd6fo.png)

## 2.2 规则二
如果元素是向左(右)浮动，浮动元素的左(右)边界不能超出包含块的左(右)边界

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723538866000zlo18m.png)

## 2.3 规则三

**浮动元素之间不能层叠**

* 如果一个元素浮动，另一个浮动元素已经在那个位置了，后浮动的元素将紧贴着前一个浮动元素(左浮找左浮，右浮找右浮)
* 如果水平方向剩余的空间不够显示浮动元素，浮动元素将向下移动，直到有充足的空间为止

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723539373000zupikk.png)


```html
<style>
	.box {
		width: 500px;
		height: 500px;
		margin: 0 auto;
		background-color: red;
	}
	.box .item1 {
		width: 200px;
		height: 200px;
		background-color: blue;
		float: left;
	}
	.box .item2 {
		width: 200px;
		height: 200px;
		background-color: darkmagenta;
		float: left;
	}
	.box .item3 {
		width: 200px;
		height: 200px;
		background-color: orange;
		float: left;
	}
</style>

<div class="box">
	<div class="item1">1</div>
	<div class="item2">2</div>
	<div class="item3">3</div>
</div>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17235505320006ov2nc.png)

## 2.4 规则四
**浮动元素不能与行内级内容层叠，行内级内容将会被浮动元素推出**

* 比如行内级元素、inline-block元素、块级元素的**文字内容**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723551089000n90opy.png)

## 2.5 规则五
**行内级元素、inline-block元素浮动后，其顶部将与所在行的顶部对齐**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723551155000ch7i4u.png)


# 三、浮动练习
## 3.1 浮动练习一
**浮动常用的场景**

* 解决行内级元素、inline-block元素的水平间隙问题[[01 行内级之间的间隙]]

**百度页数的选择：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723556172000f9z864.png)


```html
<style>
	/* 样式重置 */
	body {
		padding: 0;
		margin: 0;
	}
	ul,li {
		list-style: none;
		padding: 0;
		margin: 0;
	}
	a {
		text-decoration: none;
		color: #fff
	}
	/* 样式设置 */
	ul > li > a {
		float: left;
		width: 36px;
		height: 36px;
		line-height: 36px;
		text-align: center;************
		background-color: orange;
		border-radius: 6px;
		margin-left: 5px;
	}
	ul > li > a:hover,ul > li > .none{
		background-color: darkorchid;
		color: aqua;
	}
	ul > li > a.item {
		width: 50px;
	}
</style>

<ul>
	<li><a href="#">1</a></li>
	<li><a href="#">2</a></li>
	<li><a href="#">3</a></li>
	<li><a href="#">4</a></li>
	<li><a href="#">5</a></li>
	<li><a href="#">6</a></li>
	<li><a class="none" href="#">7</a></li>
	<li><a href="#">8</a></li>
	<li><a href="#">9</a></li>
	<li><a href="#">10</a></li>
	<li><a class="item" href="#">下一页&gt;</a></li>
	<!-- 大于号使用字符实体 -->
</ul>
```

## 3.2 浮动练习二
**京东购物列表：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723559619000p96z18.png)


```html
<style>
	/* 重置样式 */
	body {
		padding: 0;
		height: 0;
	}
	/* 样式设置 */
	.content {
		width: 1190px;
		height: 800px;
		background-color: orange;
		margin: 0 auto;
	}
	.box {
		/* 父元素宽度=子元素宽度+margin-left+margin-right */
		margin-right: -10px;
	}
	.box .item {
		width: 230px;
		height: 342px;
		float: left;
		/* 块级元素之间尝试空隙 */
		margin-right: 10px;
	}
	.box .item1 {
		background-color: red;
	}
	.box .item2 {
		background-color: darkcyan;
	}
	.box .item3 {
		background-color: darkgreen;
	}
	.box .item4 {
		background-color: lightcoral;
	}
	.box .item5 {
		background-color: black;
	}
</style>

<div class="content">
	<div class="box">
		<div class="item item1">1</div>
		<div class="item item2">2</div>
		<div class="item item3">3</div>
		<div class="item item4">4</div>
		<div class="item item5">5</div>
	</div>
</div>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723559582000fkh9rk.png)


**我们先进行一个计算：**

content 的宽度是 1190 ，而 box 作为 content 的子级，继承的宽度也为 1190

box 盒子里面内容的宽度是：
```
item1 + item2 + item3 + item4 + item5 + margin-right*5 
=230+230+230+230+230+10*5
=1200
```

**这是为什么呀?为什么我们 box 盒子的宽度是 1190 而盒子里面内容的宽度确实 1200?**

* 我们要知道有这样一个公式：
	*  父级元素宽度=子级元素宽度+margin-left+margin-right
*  按照上面的理解，带入content和box数值看一看
	* 1190=box元素宽度+0+-10
* 这样一看突然发现只有 box 元素宽度为 1200 时，公式才满足
	* 这里就把 box 的宽度变为 1200 了
	* 因为没有设置过 box 的宽度，而 box 原本宽度 1190 是继承 content 的宽度，而继承的权重是很小的，所以后面通过这是 margin-right:-10px; 可以改变 box 原本的宽度。

## 3.3 浮动练习三

**京东的购物：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723637156000zrkjm6.png)

```html
<style>
	.content {
		width: 1190px;
		height: 1000px;
		background-color: orange;
		margin: 0 auto;
	}
	.content .wrapper {
		margin-right: -10px;
	}
	.content .item {
		width: 290px;
		background-color:aqua;
		float: left;
		margin-bottom: 10px;
		margin-right: 10px;
	}
	.content .left {
		height: 370px;
	}
	.content .right {
		height: 180px;
	}
</style>

<div class="content">
	<div class="wrapper">
		<div class="item left"></div>
		<div class="item left"></div>
		<div class="item right"></div>
		<div class="item right"></div>
		<div class="item right"></div>
		<div class="item right"></div>
	</div>
</div>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723637701000tjekr4.png)

## 3.4 浮动练习四
考拉的购物布局-里面存在[[12 CSS的盒子模型（Box Model）#五、边框-brder|boder]]：（非常难理解的东西）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17236463190004d586e.png)


```html
<style>
	.content {
		width: 1100px;
		height: 500px;
		background-color:red;
		margin: 0 auto;
	}
	.item {
		float: left;
		width: 221px;
		height: 300px;
		background-color: orange;
		border:1px black solid;
		box-sizing: border-box;
		margin-right: -1px;
	}
	.box .fist {
		width: 220px;
	}
</style>

<div class="content">
	<div class="box">
		<div class="item fist"></div>
		<div class="item"></div>
		<div class="item"></div>
		<div class="item"></div>
		<div class="item"></div>
	</div>
</div>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/172364618200038s2fk.png)


**边框的问题首先需要知道，加上边框后的宽度到底是多少：**^float-boder

默认情况下是 content-box，所以在进行边框的添加时需要把[[12 CSS的盒子模型（Box Model）#十一、CSS属性 box-sizing|box-sizing]]设置为 boder-box。

**其次是添加边框的时候会有边框重复的问题，这里可以使用两种方法来解决：**

* 第一种是变重复的边框去除一边边框
* 第二种是让两个重复的元素，使用margin的负值，覆盖掉另一个重复的边框。

**最后是进行了margin负值的一个覆盖，子元素整体就会小于父元素 1px 的值：**

* 通过增加每一个子元素 1px 就可以解决这个问题。

> [!tip] margin 各种变化的计算：
> 当两个子元素的宽度或者高度都为 a ，并且父元素的高度或者宽度为 b+1 ，则`a+a < b+1`。
> 进行添加边框（1px）后（默认情况下 box-sizing=content-box）两个子元素总的高度或者宽度为 `a+2+a+2 > b+1`，就会超出 b+1 的范围。
> 对每个子元素设置 box-sizing = boder-box 后，padding、border都布置在width、height里边，这个时候子元素总的高度或者宽度为 `a+a < b+1`，b+1 元素就可以包含了两个子元素，**但是还是会存在 1px 的空间。**
> 子元素存在边框的重叠部分，进行margin负值消除重叠边框后的高度或者宽度为 `a-1+a<b+1`，**这样会存在 2px 的空间。**
> **这个时候我们对每个子元素宽度或者高度增加 1px ：**
> * 其中被覆盖过子元素 a-1 在原有的基础上增了 1px （a-1+1=a），最终经过上面的变化最终大小为 a 。
> * 其中另一个子元素也增加了 1px （a+1px）
> * 最终连个子元素的总高度和宽度 `a+a+1=b+1`


# 四、浮动的问题

## 4.1 高度塌陷
**由于浮动元素脱离了标准流，变成了脱标元素，所以不再向父元素汇报高度**

* 父元素计算总高度时，就不会计算浮动子元素的高度，导致了高度坍塌的问题

**解决父元素高度坍塌问题的过程，一般叫做清浮动(清理浮动、清除浮动)**

**清浮动的目的是**

* 让父元素计算总高度的时候，把浮动子元素的高度算进去

**使用 CSS 属性-clear：**

**clear属性是做什么的呢?**

* clear 属性可以指定一个元素是否必须移动(清除浮动后)到在它之前的浮动元素下面;

**clear的常用取值**

* left:要求元素的顶部低于之前生成的所有左浮动元素的底部
* right:要求元素的顶部低于之前生成的所有右浮动元素的底部
* both:要求元素的顶部低于之前生成的所有浮动元素的底部
* none:默认值，无特殊要求

**那么我们可以利用这个特性来清除浮动**

```html
<style>
	.content {
		width: 1190px;
		background-color: orange;
		margin: 0 auto;
	}
	.content .wrapper {
		margin-right: -10px;
	}
	.content .item {
		width: 290px;
		background-color:aqua;
		float: left;
		margin-bottom: 10px;
		margin-right: 10px;
	}
	.content .left {
		height: 370px;
	}
	.content .right {
		height: 180px;
	}
	.content .line {
		height: 10px;
		background-color: red;
		clear:both;
	}
	.ducent {
		height: 300px;
		background-color: blue;
	}
</style>

<div class="content">
	<div class="wrapper">
		<div class="item left"></div>
		<div class="item left"></div>
		<div class="item right"></div>
		<div class="item right"></div>
		<div class="item right"></div>
		<div class="item right"></div>
		<div class="line"></div>
	</div>
	<div class="ducent"></div>
</div>
```

> 没有给 warpper 设置高度，而内容里面的 item 是一个浮动元素脱离标准流，所以不会给父级的祖先元素汇报高度，这样的话 line 是在顶部出现的，而对 line 设置 clear:both; 这样的话它就会在 浮动元素的下面显示了，后面的 ducent 就会紧跟着 line ，这样的话就解决了浮动高度塌陷的问题。

**真实开发中 line 是不会设置高度和颜色的。**

> [!tip] 不足之处
> 这是是 CSS 浮动产生的高度塌陷，而我们解决确实使用一个 html 的 div 来进行解决，这一个 结构（html）和样式（CSS）并没有分离开来。
> 本来是 CSS 产生的问题，我们却要使用 html 来进行解决，**违背了样式和结构的分离。**

**最终的解决方案如下：**

* 使用[[10 伪元素（pseudo-elements）|伪元素]]
* 给父元素增加::after伪元素
* 纯CSS样式解决，结构与样式分离(推荐)

```html
<style>
	.content {
		width: 1190px;
		background-color: orange;
		margin: 0 auto;
	}
	.content .wrapper {
		margin-right: -10px;
	}
	.content .item {
		width: 290px;
		background-color:aqua;
		float: left;
		margin-bottom: 10px;
		margin-right: 10px;
	}
	.content .left {
		height: 370px;
	}
	.content .right {
		height: 180px;
	}
	.clear_fix::after {
		/* 伪元素必须有内容 */
		content: "";
		clear: both;
		/* 伪元素是行内级元素(内容没有就没有宽度) */
		display: block;
		/* 浏览器的兼容(固定) */
		visibility: hidden;
		height: 0;
	}
	.clear_fix {
		/* 兼容IE6/7浏览器 */
		*zoom: 1;
	}
	.ducent {
		height: 300px;
		background-color: blue;
	}
</style>


<div class="content">
	<div class="wrapper clear_fix">
		<div class="item left"></div>
		<div class="item left"></div>
		<div class="item right"></div>
		<div class="item right"></div>
		<div class="item right"></div>
		<div class="item right"></div>
	</div>
	<div class="ducent"></div>
</div>
```


