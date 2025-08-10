# 一、认识绝对定位
**元素脱离normal flow(脱离标准流、脱标)**

**可以通过left、right、top、bottom进行定位**

* 定位参照对象是**最邻近的定位祖先元素**
* 如果找不到这样的祖先元素，**参照对象是视口**

> [!tip] 定位元素(positioned element)
> * position值不为static的元素
> * 也就是position值为relative、absolute、fixed的元素

# 二、案例练习
**父盒子里面包含子盒子，子盒子里面包含内容：**

```html
<style>
	.box {
		width: 800px;
		height: 700px;
		background-color: red;
		/* 相对定位 */
		position: relative;
	}
	.content {
		width: 400px;
		height: 400px;
		background-color: orange;
		position: absolute;
		bottom: 0;
		right: 0;
	}
	strang {
		/* 绝对定位，是相对与最近定位的祖先元素
		所以是相对与 .content 进行定位的*/
		position: absolute;
		bottom: 0;
		left: 0;
		color: blue;
	}
</style>

<div class="box">
	<div class="content">
		<div>我是div元素</div>
		<strang>我是strang元素</strang>
		<div>呵呵呵</div>
	</div>
</div>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723451992000igxhke.png)

# 三、绝对定位元素的特点
> 需要知道的是，这里的据对定位元素是指 absolute 和 fixed 的，
> 而 position 设置的是定位元素。
> 所以 absolute 和 fixed 是定位元素，并且是绝对定位元素。

**可以随意设置宽高，宽高默认由内容决定**

* 要注意的是：这样虽然具有了line-black的特性，但是并不是行内块级元素。

**不再受标准流的约束**

* 不再严格按照从上到下、从左到右排布
* 不再严格区分块级、行内级，块级、行内级的很多特性都会消失

**不再给父元素汇报宽高数据**

**脱标元素内部默认还是按照标准流布局**

```html
<style>
	.box {
		background-color: red;
	}
	strong {
		position: absolute;
		/* 绝对定位元素就不会把宽高
		汇报给父元素 .box */
	}
</style>
<div class="box">
	<strong>我是strong元素</strong>
</div>
```

**脱标元素内部默认还是按照标准流布局**

**绝对定位元素(absolutely positioned element)**

* position值为absolute或者fixed的元素

**对于绝对定位元素来说**

* 定位参照对象的宽度 = left + right + margin-left + margin-right + 绝对定位元素的实际占用宽度
* 定位参照对象的高度 =top +bottom + margin-top+ margin-bottom + 绝对定位元素的实际占用高度


**如果希望绝对定位元素的宽高和定位参照对象一样，可以给绝对定位元素设置以下属性**

* left:0、right:0、top:0、bottom: 0、margin:0

**如果希望绝对定位元素在定位参照对象中居中显示，可以给绝对定位元素设置以下属性**

* left: 0、right: 0、top:0、bottom: 0、margin: auto
* 另外，还得设置**具体的宽高值**(宽高小于定位参照对象的宽高)

```html
<style>
	.box {
		width: 700px;
		height: 400px;
		background-color: red;
		position: relative;
	}
	.content {
		width: 200px;
		height: 100px;
		background-color: orange;
		position: absolute;
		right: 0;
		bottom: 0;
		left: 0;
		top: 0;
		margin: auto;
	}
</style>

<div class="box">
	<div class="content"></div>
</div>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723464484000omqct3.png)





