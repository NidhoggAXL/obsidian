# 一、认识函数
**在前面有使用过很多个CSS函数:**

* 比如rgb/rgba/translate/rotate/scale等;
* CSS函数通常可以帮助我们更加灵活的来编写样式的值，

**下面我们再学习几个非常好用的CSS函数**:

* var: 使用CSS定义的变量;
* calc: 计算CSS值, 通常用于计算元素的大小或位置;
* blur: 毛玻璃(高斯模糊)效果;
* gradient:颜色渐变函数;


# 二、var
**var**:variable(变量)

**CSS中可以自定义属性**

* 属性名需要以两个减号(--)开始;
* 属性值则可以是任何有效的CSS值

```html
<style>
	div {
		--main-color: red;
	}
</style>
```

可以通过 var 函数来使用：

```html
<style>
	div {
		--main-color: red;
	}
	
	.box {
		color: var(--main-color);
	}
</style>
<body>
	 <div class="box">
		我是 div 元素
	 </div>
</body>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1726316953000gjso0b.png)

规则集定义的选择器,是自定义属性的可见作用域(只在选择器内部有效)

* 所以推荐将自定义属性定义在html中，也可以使用:root 选择器

```html
<style>
	:root {
		--main-color: red;
	}
	html {
		--main-color: red;
	}
</style>
```

# 三、calc
**calc**:calculate(计算)

**calc()函数允许在声明 CSS 属性值时执行一些计算。**

* 计算支持**加减乘除**的运算;
	* + 和 - 运算符的两边**必须要有空白字符**
* 通常用来**设置一些元素的尺寸或者位置**

# 四、blur

**blur()函数将高斯模糊应用于输出图片或者元素;**

* blur(radius)
* radius, 模糊的半径, 用于定义高斯函数的偏差值, 偏差值越大, 图片越模糊;

radius - 半斤    blur - 模糊

**通常会和两个属性一起使用:**

* filter: 将模糊或颜色偏移等图形效果应用于元素:
* backdrop-filter: 为**元素或者背景后面的区域添加模糊或者其他效果,**
	* 根据函数的意思可以知道是**背部的后面**，可以理解为最底层
	* 因为它适用于元素背后的所有元素，为了看到效果，**必须使元素或其背景至少部分透明。**

**fiter的使用：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1726319325000tyd0xj.png)

> fiter 是有继承性的，上面的例子也可以对 box 进行设置

**backdrop-filter的使用：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1726319577000debcar.png)

> backdrop-filter 是最底层的，**对这个属性进行设置的时候必须有添加背景或者元素。**
2
# 五、gradient（了解）
gradient - 渐变

**`<gradient>`是一种`<image>CSS`数据类型的子类型，用于表现两种或多种颜色的过渡转变。**

* CSS的`<image>`数据类型描述的是**2D图形**;
* 比如background-image、list-style-image、border-image、content等;
* `<image>`常见的方式是通过url来引入一个图片资源;
* 它也可以通过CSS的`<gradient>`函数来设置颜色的渐变,

**`<gradient>`常见的函数实现有下面几种:**

* linear-gradient():创建一个表示两种或多种颜色**线性渐变**的图片;
* radial-gradient():创建了一个图像，该图像是由从原点发出的两种或者多种颜色之间的逐步过渡组成,
* repeating-linear-gradient():创建一个由重复线性渐变组成的`<image>`;
* repeating-radial-gradient():创建一个重复的原点触发渐变组成的`<image>`;
* 等等;

radial - 辐射

> 这里的渐变有很多种的编写方式，可以进行文档查询

> [!tip] 特别注意
> 这里的gradient组成的是一张**图片**。



