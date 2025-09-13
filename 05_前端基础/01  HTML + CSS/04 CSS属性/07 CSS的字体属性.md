# 一、font-size(重要)

**font-size决定文字的大小**

**常用的设置:**

* 具体数值+单位
	* 比如100px
* 也可以使用em单位(不推荐):1em代表100%，2em代表200%，0.5em代表50%

**百分比:**

* 基于父元素的font-size计算，比如50%表示等于父元素font-size的一半

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711614215000je9uos.png)

需要知道的是font-size 是具有继承性的，所以这里是可以使用%来进行使用的，但是他到底继承的是什么，这个就需要取查询文档了。

> 通过查询文档知道，font-size的继承的是上一层的font-size
> 所以这里百分比的大小是先对于40px的70%的。

# 二、font-family(重要，不过一般仅设置一次)\

**font-family用于设置文字的字体名称:**

* 可以设置1个或者多个字体名称
* 浏览器会选择列表中第一个该计算机上有安装的字体;
* 或者是通过 @font-face 指定的可以直接下载的字体

```html
<style>
body {
  /* 对body里面的字体进行设置 */
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}
</style>
```


# 三、font-weight(重要)
font-weight用于设置文字的粗细](重量)

**常见的取值:**

* `100|200|300|400|500|600|700|800|900`:每一个数字表示一个重量
* normal:等于400
* bold:等于700
 
**strong、b、h1~h6 等标签的font-weight默认就是bold**

> normal  正常
> bold  明显的

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711626547000bb2v5o.png)

# 四、font-style(一般)
**font-style用于设置文字的常规、斜体显示:**

* normal:常规显示
* italic(斜体):用字体的斜体显示(通常会有专门的字体)
* oblique(倾斜):文本倾斜显示(仅仅是让文字倾斜)

**em、i、cite、address、var、dfn等元素的font-style默认就是italic**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711627055000whtfyk.png)


# 五、font-variant(基本不用)
**font-variant可以影响小写字母的显示形式:**

* variant是变形的意思,

**可以设置的值如下:**

* normal:常规显示
* small-caps:将小写字母替换为缩小过的大写字母

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711627307000ly10xy.png)

# 六、font-heigth(重要)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714635924000azc22c.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714636802000o4avzr.png)

> 运用 line-height 就相当于 字体的高度 = line-height - 行距

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714637105000i4tz7g.png)

## 小结
这里的 line-height 是对文本自己本身的一个操作，对于你给它的块级元素是没有关系的。

### 举例1：
给一个块级元素 100px 文本的 line-height 300px 

```html
<style>
	.box {
	  bakground-color:red;
	  height: 100px;
	  line-height: 300px;
	}
</style>

<div class="box">我是div块级元素</div>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714637545000axz9mk.png)

> * 文本跳出的 div 块级元素的模块

### 举例2：
让文本居中显示：让 `line-height = height` 时居中显示

```html
<style>
.box {
  background-color:red;
  height: 100px;
  line-height: 100px;
}
</style>

<div class="box">我是div块级元素</div>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171463772700004d4mv.png)


### 举例3：
利用line-height 的继承性对块级与行内非替换元素进行设置区分。

对**块级元素的父级元素**设置大于内容高度的line-height值：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17240789870006a64k3.png)

> 父级元素会被撑起来

对**行内块级元素的父级元素**设置大于内容高度的line-height值：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1724079098000a3wat4.png)

> 父级元素也会被撑起来

对**行内非替换元素的父级**元素设置大于内容高度的line-height值：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1724079226000nc10lm.png)

> 可以发现父级元素是不会撑起来的，但是它的行高还是会增加。

### 举例4：
line-height 具有继承属性，line-height是字体内容进行设置的，但是如果继承者是一个没有内容的，也不会继承这个属性。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1724159855000kduvmn.png)

> line-height 具有继承性，但是 content 并没有设置内容，就不会继承父级元素的 line-height

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17241599690006bete8.png)

> content 里面有内容，就会继承父级元素的 line-height 

# 七、font
**font是一个缩写属性：**

* font 属性可以用来作为 font-style, font-variant, font-weight,font-size, line-height 和 font-family 属性的简写,
* 语法：`font-style font-variant font-weight font-size/line-height font-family`

**规则:**

* font-style、font-variant、font-weight可以随意调换顺序，也可以省略
* /line-height可以省略，如果不省略，必须跟在font-size后面
* font-size、font-family不可以调换顺序，不可以省略

```html
<style>
	/* 关于字体属性 */
	.box{
	  font-size: 30px;
	  font-weight: 500;
	  font-variant: small-caps;
	  font-style: normal;
	  font-family: serif;
	  line-height: 30px;
	
	  /* 属性缩写 */
	  font: normal small-caps 500 30px/30px serif;
}
</style>
```

## 7.1 缩写属性中也可以对 line-height 直接编写数值
```html
  <style>
    /* 关于字体属性 */
    .box{
      font-size: 30px;
      font-weight: 500;
      font-variant: small-caps;
      font-style: normal;
      font-family: serif;
      line-height: 30px;
  
      /* 属性缩写 */
      font: normal small-caps 500 30px/30px serif;
      /* 1.5行高是相对于 font-size 的 */
      font: normal small-caps 500 30px/1.5 serif;
    }
  
  </style>
</head>

<body>
  <div class="box">我是div跨级元素/div>
</body>
</html>
```

# 八、文字阴影 text-shadow
`text-shadow`用法类似于[[12 CSS的盒子模型（Box Model）#九、盒子阴影 box-shadow|box-shadow]]，用于给文字添加阴影效果.

**与box-shadow的区别：**
* 没有衍生（spread-radius）和向内（insert）
* 查看文字阴影和盒子阴影在同一个网站







