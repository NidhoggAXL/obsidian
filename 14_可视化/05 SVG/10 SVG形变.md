# 一、形变-transform

transform 属性用来定义元素及其子元素的形变的列表。 

- 此属性可以与任何一个 SVG 中的元素一起使用。如果使用了变形，会在该元素内部建立了一个新的坐标系统。 
- **从 SVG2 开始，transform它是一个 Presentation Attribute**，意味着它可以用作 CSS 属性。 
- 但是transform作为CSS 属性和元素属性之间的语法会存在一些差异。 
	- **比如作为元素属性时：支持2D变换，不需单位，rotate可指定旋转原点。**

transform属性支持的函数： 

- translate(x， y) 平移。 
- **rotate(z) / rotate(z， cx，cy) ：旋转。** 
- scale（x, y） ：缩放 
- skew(x, y) ：倾斜。 
- matrix(a, b, c, d, e) ： `2*3` 的形变矩阵 

>[!tip] 注意：形变会不会修改坐标系？
>
> 会，形变元素内部会建立一个新的坐标系，后续的绘图或形变都会参照新的坐标系。

# 二、平移-trranslate

**平移**：把元素移动一段距离， 使用transform属性的 translate()函数来平移元素。 

- 与CSS的translate相似但有区别，这里**只支持2D变换，不需单位**。 

translate(x, y)函数 

- 一个值时，设置x轴上的平移，而第二个值默认赋值为 0
- 二个值时，设置x轴和y轴上的平移 

**平移案例**：将一个矩形由默认的（0,0）点，移到点 (30,40)。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17586831820000tep33.png)

> [!tip] 注意：平移会不会修改坐标系？ 
> 
> 会，元素内部会建立一个新的坐标系。

# 三、旋转-rotate

**旋转**：把元素旋转指定的角度， 使用transform属性的 rotate(deg，cx, cy) 函数来旋转元素。 

- 与CSS的rotate相似但有区别。**区别是：只支持2D变换，不需单位，可指定旋转原点。**

**rotate(deg, cx, cy) 函数：**

- 一个值时，设置z轴上的旋转的角度。
- 三个值时，后面两个参数表示旋转的原点（**相对于自身**）。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758683640000a1xikv.png)

> [!tip] 注意： 
> 
> - 旋转会不会修改坐标系？ 会，坐标轴也会跟着旋转了 
> - 如何指定旋转原点？ 直接在rotate中指定 cx ,cy（相对于自身）； 或者使用CSS样式写动画。

# 四、缩放-scale

缩放：改变元素尺寸，使用transform属性的 scale() 函数来缩放元素。 

- 与CSS的scale相似但有区别，这**只支持2D变换，不需单位**。 

scale(x, y)函数 

- 一个值时：第二个数字被忽略了，它默认等于第一个值。
- 二个值时：它需要两个数字，作为比率计算如何缩放。**0.5 表示收缩到 50%**。 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17586840210004ife3e.png)

> [!tip] 注意： 
> 
> - 缩放会不会修改坐标系？会，坐标轴被缩放了。 
> - 如何指定缩放的原点？ SVG属性实现需要 **平移坐标** 和 **移动图形** 了；或者 直接使用CSS来写动画

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758684453000ovl0in.png)



