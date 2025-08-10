# 一、认识单位

前面编写的CSS中，我们经常会使用px来表示一个长度(大小)，比如font-size设置为18px，width设置为100px。

**px是一个长度(length)单位，事实上CSS中还有非常多的长度单位。**

**整体可以分成两类**:

* 绝对长度单位(Absolute length units);
* 相对长度单位(Relative length units):

# 二、CSS绝对单位
**绝对单位:**

* 它们与其他任何东西都没有关系，通常被认为总是相同的大小。
* 这些值中的大多数在用于**打印时**比用于屏幕输出时更有用，例如，我们通常不会在屏幕上使用cm。
* **惟一一个经常使用的值，就是px(像素)。**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1726387197000rfvmc4.png)

# 三、CSS相对单位

**相对长度单位**

* 相对长度单位相对于其他一些东西，
* 比如父元素的字体大小，或者视图端口的大小;
* 使用相对单位的好处是，经过一些仔细的规划，您可以使文本或其他元素的大小与页面上的其他内容相对应;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1726401141000enwfuc.png)

**em 在官方的文档中并没有说过是相对父元素，只说过是相对自己的字体大小。**

```css
	.container {
		font-size: 20px;
	}
	
	.container .box {
		width: 5em;
		height: 2em;
		background-color: orange;
	}
```

上面代码中的 box 中的 font-size 的 em 是父元素的字体大小

但是其中的根本其实是对 box 的 fon-size 是先继承了 container 的字体大小 20px ，后买的宽度和高度的设置是 继承过来作为自己的 font-size 为单位进行设置的。





