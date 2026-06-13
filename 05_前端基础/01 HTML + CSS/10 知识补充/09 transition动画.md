# 一、认识transition动画

**transition - 过渡**


**什么是transition动画呢?**

* css transitions提供了一种在更改cs属性时控制**动画速度的方法**。
* 可以让CSS属性变化成为一个**持续一段时间**的过程，而**不是立即生效**的;
* 比如将一个元素从**一个位置移动到另外一个位置**，默认在修改完CSS属性后会立即生效;
* 但是我们可以通过CSS transition，让这个过程加上一定的动画效果，包括一定的**曲线速率变化;**

通常将两个状态之间的过渡称为隐式过渡(implicit transitions)，因为开始与结束之间的状态由**浏览器决定。**

**CSS transitions可以决定**

* 哪些属性发生动画效果 (明确地列出这些属性)
* 何时开始(设置 delay)
* 持续多久(设置 duration)
* 如何动画(定义timingfunction，比如匀速地或先快后慢)。

# 二、那些CSS属性
并非所有的CSS属性都可以执行动画的，那么我们如何知道哪些属性支持动画呢?

**方法一**:在MDN可执行动画的CSS属性中查询


**方法二**:阅读CSS属性的文档说明

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17252783810009csxm6.png)


# 三、transition-过渡动画

transition CSS 属性是 transition-property, transition-duration,transition-timing-function 和 transition-delay 的一个简写属性。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725279425000z7ka1c.png)

| 英文       | 翻译          |
| -------- | ----------- |
| property | 财产、地产/属性、性质 |
| duration | 持续时间/持续     |
| timing   | 时机          |
| function | 函数          |
| delay    | 延迟          |

**transition-property:指定应用过渡属性的名称**

* all（默认）:所有属性都执行动画:
* none:所有属性都不执行动画;
* CSS属性名称:要执行动画的CSS属性名称，比如width、left、transform等
	* 一般情况下动画都会进行一个持续时间的设置，所以比起其他瞬间变化的要慢一点。

**transition-duration：指定过渡的持续时间**

* 单位可以是秒(s)或毫秒(ms)
* 1s=1000ms
* 默认0

**transition-timing-function：指定过渡的时间速率变化**

* https://developer.mozilla.ora/zh-CN/docs/Web/csS/transition-timing-function
* 默认ease

**transition-delay：指定了发生过渡前延迟的时间**

* 默认为0

```css
<style>
	.box {
		position: relative;
		width: 200px;
		height: 100px;
		left: 0;
		background-color: orange;

		/* transition-property: left  width;
		transition-property: left , width;
		transition-property: left; */
		transition-property: all;
		transition-duration: 3s;
		transition-timing-function: ease-in-out;
		transition-delay: 1s;
	}
	.box:hover {
		height: 200px;
		width: 500px;
		left: 100px;
		transform:translate(100px , 0 );
		background-color: red;
	}
</style>

<div class="box"></div>
```

# 四、transition缩写
语法：

```html
transition = 
  <single-transition>#  

<single-transition> = 
  [ none | <single-transition-property> ]  ||
  <time>                                   ||
  <easing-function>                        ||
  <time>
```

`||`或组合符，必须存在一个或者多个，顺序不限。

```css
transition: all 3s ease-in 3s;
```

# 五、transition缺点

使用 trandition 过渡动画存在一下缺点：

* transition**只能定义开始状态和结束状态**，不能定义中间状态，也就是说只有两个状态;
* transition**不能重复执行**，除非一再触发动画;
* transition需要在**特定状态下会触发才能执行**，比如某个属性被修改了，

如果我们希望可以有**更多状态**的变化，我们可以使用[[10 animation动画]]。

