# 一、认识路径

什么是路径？ 

- 图形的基本元素是路径。路径是通过不同颜色和宽度的线段或曲线相连形成的不同形状的点的集合。 
- 路径是可由很多子路径构成，这些子路径都是在一[]()个列表中，列表中所有子路径（线、弧形等）将构成图形。 
- 一个路径，甚至一个子路径，**通常都是闭合的**。 

使用路径绘制图形的步骤： 

1. 首先需要创建路径起始点（beginPath）。 
2. 然后使用画图命令去画出路径( arc 、lineTo )。 
3. **之后把路径闭合( closePath , 不是必须，但是建议都编写)**。 
4. 一旦路径生成，就能通过描边(stroke)或填充路径区域(fill)来渲染图形。 

以下是绘制路径时，所要用到的函数 

- **beginPath()**：新建一条路径，生成之后，图形绘制命令被指向到新的路径上绘图，不会关联到旧的路径。 
- **closePath()**：闭合路径之后图形绘制命令又重新指向到 beginPath之前的上下文中。 
- **stroke()**：通过线条来绘制图形轮廓/描边（针对当前路径图形）。 
- **fill()**：通过填充路径的内容区域生成实心的图形（针对当前路径图形）。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758251481000m878gy.png)

# 二、绘制直线

移动画笔（moveTo）方法 

- moveTo 方法是不能画出任何东西，但是它也是路径列表的一部分 
- moveTo 可以想象为在纸上作业，一支钢笔或者铅笔的笔尖从一个点到另一个点的移动过程。 
- **moveTo(x, y)： 将笔移动到指定的坐标 x 、 y 上。** 
- 当 canvas 初始化或者beginPath()调用后，我们通常会使用moveTo(x, y)函数设置起点。 
- 使用moveTo函数能够绘制一些不连续的路径。

**绘制直线（lineTo）方法**

- **lineTo(x, y)**： 绘制一条从当前位置到指定 (x ，y)位置的直线。 
	- 该方法有两个参数(x ， y)代表坐标系中直线结束的点。 
	- 开始点和之前的绘制路径有关，之前路径的结束点就是接下来的开始点。 
	- 当然开始点也可以通过moveTo(x, y)函数改变。 

绘制一条直线

- 第一步：调用 beginPath() 来生成路径。本质上，路径是由很多子路径（线、弧形、等）构成。 
- 第二步：调用moveTo、lineTo函数来绘制路径（路径可以是连续也可以不连续）。 
- 第三步：闭合路径 closePath()，虽然不是必需的，但是**通常都是要闭合路径。** 
- 第四步：调用stroke()函数来给直线描边。

# 三、绘制三角形(Triangle)

绘制一个三角形步骤 

- 第一步：调用 beginPath() 来生成路径。 
- 第二步：调用moveTo()、lineTo()函数来绘制路径。 
- 第三步：闭合路径 closePath()，不是必需的。 
	- closePath() 方法会通过绘制一条从当前点到开始点的直线来闭合图形。 
	- 如果图形是已经闭合了的，即当前点为开始点，该函数什么也不做。 
- 第四步：调用stroke()函数来给线描边，或者调用fill()函数来填充（**使用填充 fill 时，路径会自动闭合，而 stroke 不会**）。

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758265709000bmg1z6.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758265718000pq3mt1.png)

如果使用 fill() 函数来填充：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758265800000u5d6of.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758265808000lxcnfz.png)


# 四、绘制圆弧(Arc)、圆(Circle)

**绘制圆弧或者圆，使用arc()方法。** 

- arc(x, y, radius, startAngle, endAngle, anticlockwise)，该方法有六个参数：
- x、y：为绘制圆弧所在圆上的圆心坐标。 
- radius：**为圆弧半径**。 
- startAngle、endAngle：该参数用弧[]()度定义了开始以及结束的弧度。这些都是以 x 轴为基准。 
- anticlockwise：为一个布尔值。为 true ，是逆时针方向，为false，是顺时针方向，默认为false。 

**认识弧度**：弧度(英语:radian)，是平面角的单位。1单位弧度为:圆弧长度等于半径时的圆心角，而一个完整的圆的弧度是 `Math.Pl*2`，半圆弧度是 Math.Pl

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17582668250005duksd.png)


**计算弧度**:

- arc() 函数中表示角的单位是弧度，不是角度。 
- 角度与弧度的 JS 表达式：**弧度=( Math.PI / 180 ) * 角度 ，即 1角度= Math.PI / 180 个弧度**
	- 比如：旋转90°：Math.PI / 2； 旋转180°：Math.PI ； 旋转360°：Math.PI * 2； 旋转-90°：-Math.PI / 2；

绘制一个圆弧的步骤 

- 第一步：调用 beginPath() 来生成路径。 
- 第二步：调用arc()函数来绘制圆弧。 
- 第三步：闭合路径 closePath()，**不是必需的**。 
- 第四步：调用stroke()函数来描边，或者调用fill()函数来填充（使用填充 fill 时，路径会自动闭合）。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758266484000os5lx4.png)
[]()
![gh|200](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175826649200008nwr2.png)


# 五、绘制矩形(Rectangle)

绘制矩形的另一个方法： 

- 调用rect() 函数绘制，即将一个矩形路径增加到当前路径上 
- rect(x, y, width, height) 
	- 绘制一个左上角坐标为（x,y），宽高为 width 以及 height 的矩形。

> [!warning] 注意： 当该方法执行的时候，moveTo(x, y) 方法自动设置坐标参数（0,0）。也就是说，当前笔触自动重置回默认坐标。

![gh|400](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758267397000kkalgx.png)

![gh|200](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758267406000yftpi5.png)




# 六、色彩Colores

前面已经学过了很多绘制图形的方法。如果我们想要**给图形上色**，有两个重要的属性可以做到： 

- **fillStyle = color**： 设置图形的填充颜色，**需在 fill() 函数前调用**。 
- **strokeStyle = color**： 设置图形轮廓的颜色，**需在 stroke() 函数前调用**。 

color颜色 

- color 可以是表示 CSS 颜色值的字符串，支持：关键字、十六进制、rgb、rgba格式。 
- 默认情况下，线条和填充颜色都是黑色（CSS 颜色值 `#000000`）。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758269935000dxt1oh.png)

> [!note] 注意:
> 
> - 一旦设置了 strokeStyle 或者 fillStyle 的值，那么这个新值就会成为**新绘制的图形的默认值。** 
> - 如果你要给图形上不同的颜色，你需要重新设置 fillStyle 或 strokeStyle 的值。 

额外补充:

- fill() 函数是图形填充，fillStyle属性是设置填充色 
- stroke() 函数是图形描边，strokeStyle属性是设置描边色

# 七、透明度 Transparent

除了可以绘制实色图形，我们还可以用 canvas 来绘制半透明的图形。 

- 方式一：strokeStyle 和 fillStyle属性结合RGBA： 
- 方式二：**globalAlpha 属性** 
	- globalAlpha = 0 ~ 1 
	- 这个属性**影响到 canvas 里所有图形的透明度** 
	- 有效的值范围是 0.0（完全透明）到 1.0（完全不透明），**默认是 1.0**。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758270089000vf0nnu.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17582700930007fyerj.png)


# 八、线性Line Styles

调用lineTo()函数绘制的线条，是可以通过一系列属性来**设置线的样式**。 

- lineWidth = value： 设置线条宽度。 
- lineCap = type： 设置线条末端样式(cap-帽子)。 
- lineJoin = type： 设定线条与线条间接合处的样式。 
- .....

**lineWidth:**

- 设置线条宽度的属性值必须为正数。默认值是 1.0px，不需单位。（ 零、负数、Infinity和NaN值将被忽略） 
- 线宽是指**给定路径的中心到两边的粗细**。换句话说就是在**路径的两边各绘制线宽的一半。** 
- 如果你想要绘制一条从 (3,1) 到 (3,5)，宽度是 1.0 的线条，你会得到像第二幅图一样的结果。 
	- 路径的两边个各延伸半个像素填充并渲染出1像素的线条（深蓝色部分） 
	- 两边剩下的半个像素又会以实际画笔颜色一半色调来填充（浅蓝部分） 
	- 实际画出线条的区域为（浅蓝和深蓝的部分），填充色大于1像素了，这就是为何宽度为 1.0 的线经常并不准确的原因。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758270966000aqumr6.png)

> [!warning] 要解决这个问题，必须对路径精确的控制。如，1px的线条会在路径两边各延伸半像素，那么像第三幅图那样绘制从 (3.5 ,1) 到 (3.5, 5) 的线条，其边缘正好落在像素边界，填充出来就是准确的宽为 1.0 的线条。

**lineCap：** 属性的值决定了**线段端点显示的样子**。它可以为下面的三种的其中之一： 

- butt 截断，默认是 butt。 
- round 圆形 
- square 正方形

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758272392000sy7cgp.png)

**lineJoin：** 属性的值决定了图形中**线段连接处所显示的样子**。它可以是这三种之一：

- round 圆形 
- bevel 斜角 
- miter 斜槽规，默认是 miter。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175827243200069jq2l.png)

# 九、绘制文本

**canvas 提供了两种方法来渲染文本：** 

- **`fillText(text, x, y [, maxWidth])`** 
	- 在 (x,y) 位置，填充指定的文本 
	- 绘制的最大宽度（可选）。 
- **`strokeText(text, x, y [, maxWidth])`**
	- 在 (x,y) 位置，绘制文本边框 
	- 绘制的最大宽度（可选）。

**文本的样式（需在绘制文本前调用）** 

- font = value： 当前绘制文本的样式。这个字符串使用和 CSS font 属性相同的语法。**默认的字体是：10px sans-serif。** 
- textAlign = value：文本对齐选项。可选的值包括：start, end, left, right or center. **默认值是 start** 
- textBaseline = value：基线对齐选项。可选的值包括：**top**, hanging, **middle**, alphabetic, ideographic, **bottom**。
	- **默认值是 alphabetic**。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758272593000e0hkbg.png)

# 十、绘制图片

绘制图片，可以使用 drawImage 方法将它渲染到 canvas 里。drawImage 方法有三种形态： 

- drawImage(image, x, y) 
	- 其中 image 是 image 或者 canvas 对象，**x 和 y 是其在目标 canvas 里的起始坐标**。 
- drawImage(image, x, y, width, height) 
	- 这个方法多了 2 个参数：width 和 height，这两个参数用来控制当向 canvas 画入时应该**缩放的大小** 
- drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight) 
	- 第一个参数和其它的是相同的，都是一个图像或者另一个 canvas 的引用。其它 8 个参数最好是参照右边的图解，前 4 个 是定义图像源的切片位置和大小，后 4 个则是定义切片的目标显示位置和大小。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758272981000t33ojb.png)

图片的来源，canvas 的 API 可以使用下面这些类型中的一种作为图片的源： 

- **HTMLImageElement：这些图片是由Image()函数构造出来的，或者任何的元素。** 
- HTMLVideoElement：用一个 HTML 的 元素作为你的图片源，可以从视频中抓取当前帧作为一个图像。 
- HTMLCanvasElement：可以使用另一个 `<vanvas>` 元素作为你的图片源。
- ....

