# 一、什么是 SMIL ？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758695486000mh9qvi.png)

# 二、SVG动画的实现方式

SVG是一种基于XML的开放标准矢量图形格式，动画可以通过多种方式实现： 

- **用JS脚本实现**：可以直接通过 JavaScript 在来给 SVG 创建动画和开发交互式的用户界面。 
- **用CSS样式实现**：自 2008 年以来，CSS动画已成为WebKit中的一项功能，使得我们可以通过CSS动画的方式来给文档对象 模型(DOM) 中的 SVG 文件编写动态效果。 
- **用SMIL实现**：一种基于SMIL语言实现的SVG动画。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758695526000gq4ucn.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758695528000bir8kd.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758695532000gic3by.png)

# 三、SMIL动画的优势

SVG用SMIL方式实现动画，SMIL允许你做下面这些事情： 

- 变动一个元素的数字属性（x、y……） 
- 变动变形属性（translation 或 rotation） 
- 变动颜色属性 
- 物件方向与运动路径方向同步等等 

SMIL方式实现动画的优势： 

- 只需在页面放几个animate元素就可以实现强大的动画效果，无需任何CSS和JS代码。 
- **SMIL支持声明式动画**。声明式动画不需指定如何做某事的细节，而是指定最终结果应该是什么，将实现细节留给客户端软件 
- 在 JavaScript 中，动画通常使用 setTimeout() 或 setInterval() 等方法创建，这些方法需要手动管理动画的时间。而**SMIL 声明式动画可以让浏览器自动处理**，
	- 比如：动画轨迹直接与动画对象相关联、物体和运动路径方向、管理动画时间等等。 
- SMIL 动画还有一个令人愉快的特点是，**动画与对象本身是紧密集成的**，对于代码的编写和阅读性都非常好。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758695650000hha892.png)

# 四、Set元素

`<set>` 元素提供了一种简单的方法，可以在指定的时间内设置属性的值。 

- set元素是最简单的 SVG 动画元素。它是在经过特定时间间隔后，将属性设置为某个值（**不是过度动画效果**）。因此，**图像不是连续动画，而是改变一次属性值**。 
- 它**支持所有属性类型**，包括那些无法合理插值的属性类型，例如：字符串 和 布尔值。而对于可以合理插值的属性通常首选 `<animate>` 元素。

`<set>` 元素常用属性： 

- attributeName：指示将在动画期间更改的目标元素的 CSS 属性（ property ）或属性（ attribute ）的名称。 
- ~~attributeType~~: (已过期，不推荐)指定定义目标属性的类型（值为：CSS | XML | auto）。 
- to : 定义在特定时间设置目标属性的值。该值必须与目标属性的要求相匹配。 
	- 值类型：`<anything>`；
	- **默认值：无** 
- begin：定义何时开始动画或何时丢弃元素，默认是 0s ( begin支持多种类型的值 )。

`<set>` 案例：

1. 点击长方形后，长方形瞬间移到右边
2. 在3秒后自动将长方形瞬间移到右边


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175869796100080hd7d.png)

# 五、Animate元素

`<animate>` 元素给**某个属性创建过度动画效果**。需将animate元素嵌套在要应用动画的元素内。

`<animate>` 元素的常用属性：

- attributeName：指将在动画期间更改目标元素的 property （CSS 属）或 attribute的名称。 
- 动画值属性： 
	- from：在动画期间将被修改的属性的初始值。没有默认值。 
	- to :在动画期间将被修改的属性的最终值。没有默认值。 
	- values：该属性具有不同的含义，具体取决于使用它的上下文（没有默认值） 。 
		- 它定义了在动画过度中使用的一系列值，**值需要用分号隔开，比如：values=“2 ; 3; 4; 5”**。 
		- **当values属性定义时，from、to会被忽略。**

动画时间属性： 

- **begin**：定义何时开始动画或何时丢弃元素。默认是 0s 。 
- **dur**：动画的持续时间，**该值必须**，并要求大于 0。单位可以用小时 ( h)、分钟 ( m)、秒 ( s) 或毫秒 ( ms) 表示。 
- fill：定义动画的最终状态。 freeze（保持最后一个动画帧的状态） | remove（保持第一个动画帧的状态） 
- repeatCount：指示**动画将发生的次数**：`<number>` | indefinite。没有默认值。

> [!tip]
> 一个元素里面可以添加多个 animate 元素

```html
<svg width="400" height="400">
  <rect x="0" y="0" width="100" height="50">
    <!-- 第一个animate -->
    <animate
      attributeName="x"
      from="0"
      to="200"
      dur="2s"
    />
    <!-- 第二个animate -->
    <animate
      attributeName="y"
      from="0"
      to="300"
      dur="2s"
    />
  </rect>
</svg
```

案例：在执行完第一个动画后，在执行第二个动画（需要联合属性 id 、fill 、begin）来实现。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758699848000v4n4j7.png)

# 六、animateTransform元素

`<animateTransform>` 元素

- 指定目标元素的形变（transform）属性，从而允许控制元素的**平移、旋转、缩放或倾斜动画**（类似于 CSS3 的形变）。 
- 在一个动画元素中，只能用一个 `<animateTransform>` 元素创建动画；**存在多个时，后面会覆盖前面的动画。**

 `<animateTransform>` 元素常用属性：

- **attributeName**：指示将在动画期间更改的目标元素的 CSS 属性（ property ）或属性（ attribute ）的名称。 
- **type** ：一个指定类型的属性，在不同的使用场景下，有不同的意思： 
	- 在`<animateTransform>` 元素，只支持 **translate(x, y) | rotate(deg, cx, cy) | scale(x, y) | skewX(x) | skewY(y)** 。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758701608000t9e9xu.png)

- 动画值属性：from、to 、**values** 
- 动画时间属性：begin、**dur**、fill、repeatCount

```html
<svg width="400" height="400">
  <rect x="0" y="0" width="100" height="50">
    <animateTransform
      attributeName="transform"
      type="translate"
      values="0 0; 200 0"
      dur="2s"
      begin="1s"
      repeatCount="indefinite"
    />
  </rect>
</svg>
```
# 七、animateMotion元素

`<animateMotion>` 定义了一个元素如何沿着运动路径进行移动。

- 画元素的坐标原点，会影响元素运动路径，建议从（0, 0）开始。 
- 要复用现有路径，可在 `<animateMotion>` 元素中使用 `<mpath>` 元素。

`<animateMotion>` 元素常用属性：

- href：和对应的元素进行绑定，使其更具 animateMOtion 的定义进行移动
	- 例如：`<animateMotion href="#linePath"` ，让id为linePath的元素移动
- **path：定义运动的路径**，值和 `<path>` 元素的 d 属性一样，也可用 href 引用 一个
- **rotate ：动画元素自动跟随路径旋转**，使元素动画方向和路径方向相同
	- 值类型：<数字> | auto | auto-reverse; 
	- 默认值：0
- 动画值属性： from、to 、values 
- 动画时间属性： begin、**dur**、fill、repeatCount

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17587040970005i42go.png)



