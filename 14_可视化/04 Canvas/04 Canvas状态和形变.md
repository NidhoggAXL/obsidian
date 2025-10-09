# 一、Canvas绘画状态-保存和恢复

Canvas绘画状态 

- 是当前绘画时所产生的样式和变形的一个快照。 
- Canvas在绘画时，会产生相应的绘画状态，其实我们是可以将某些绘画的状态存储在栈中来为以后复用。 
- Canvas 绘画状态的可以调用 **save** 和 **restore** 方法是用来**保存和恢复**，这两个方法都没有参数，并且它们是**成对存在**的。


**保存和恢复（Canvas）绘画状态** 

- save()：保存画布 (canvas) 的所有绘画状态 
- restore()：恢复画布 (canvas) 的所有绘画状态

Canvas绘画状态包括： 

- 当前应用的变形（即移动，旋转和缩放） 
- 以及这些属性：**strokeStyle, fillStyle, globalAlpha, lineWidth, lineCap, lineJoin**, miterLimit, shadowOffsetX, shadowOffsetY, shadowBlur, shadowColor, **font, textAlign, textBaseline ......** 
- 当前的裁切路径（clipping path）

> [!note] 保存和恢复的状态
> 保存 save() 是保存在栈内存里面，**先进后出**，在使用 restore() 后是先调用后保存 save() 的状态

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758350713000bvslqp.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758350728000pskbsf.png)

# 二、变形Transform

Canvas和CSS3一样也是支持变形，形变是一种更强大的方法，可以将坐标原点移动到另一点、形变可以对网格进行旋转和缩放。 

**Canvas的形变有4种方法实现：** 

- **translate(x, y**)：用来移动 canvas 和它的原点到一个不同的位置。 
	- x 是左右偏移量，y 是上下偏移量（无需要单位），如右图所示。 
- **rotate(angle)**：用于以原点为中心旋转 canvas，即沿着z轴旋转。 
	- angle是旋转的弧度，是顺时针方向，**以弧度为单位**。 
- **scale(x, y)**：用来增减图形在 canvas 中像素数目，对图形进行缩小或放大。 
	- x 为水平缩放因子，y 为垂直缩放因子。如果比 1 小，会缩小图形，如果比 1 大会放大图形。默认值为 1，也支持负数。 
- transform(a, b, c, d, e, f)： 允许对变形矩阵直接修改。这个方法是将当前的变形矩阵乘上一个基于自身参数的矩阵。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17583528760008ihkko.png)

> [!tip] 注意事项： 
> - **在做变形之前先调用 save 方法保存状态是一个良好的习惯。** 
> - 大多数情况下，调用 restore 方法比手动恢复原先的状态要简单得多。 
> - 如果在一个循环中做位移但没有保存和恢复canvas状态，很可能到最后会发现有些东西不见了，因为它很可能已超出canvas画布以外了。 
> - **形变需要在绘制图形前调用**。

## 2.1 移动-translate

ranslate方法，它用来移动 canvas 和它的原点到一个不同的位置。 

- translate(x, y) 
	- x 是左右偏移量，y 是上下偏移量（无需单位）。

移动 canvas 原点的好处 

- 如不使用 translate方法，那么所有矩形默认都将被绘制在相同的（0,0）坐标原点。 
- translate方法可让我们任意放置图形，而**不需要手工一个个调整坐标值**。 

移动矩形案例 

- 第一步：先保存一下canvas当前的状态 
- 第二步：在绘制图形前translate移动画布 
- 第三步：开始绘制图形，并填充颜色

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17583530730008c9k8h.png)

## 2.2 旋转-rotate

rotate方法，它用于以原点为中心旋转 canvas，即沿着 z轴 旋转。 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758353116000dif3vd.png)


**rotate(angle) :**

- 只接受一个参数：旋转的弧度 (angle)，它是**顺时针方向**，以**弧度为单位**的值。 
- 角度与弧度的 JS 表达式：弧度=( Math.PI / 180 ) * 角度 ，即 1角度 = `Math.PI/180`  个弧度。 
- 比如：
	- 旋转90°：Math.PI / 2； 
	- 旋转180°：Math.PI ； 
	- 旋转360°：Math.PI * 2；
	- 旋转-90°：-Math.PI / 2； 
- 旋转的中心点始终是 canvas 的原坐标点，如果要改变它，我们需要用到 translate方法。

旋转案例 

- 第一步：先保存一下Canvas当前的状态，并确定旋转原点 
- 第二步：在**绘制图形前旋转画布**（坐标系会跟着旋转了） 
- 第三步：开始绘制图形，并填充颜色

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758353219000c25war.png)

## 2.3 缩放-scale

**scale方法可以缩放画布**。可用它来增减图形在 canvas 中的像素数目，对图形进行缩小或者放大。 

**scale(x, y):** 

- x 为水平缩放因子，y 为垂直缩放因子，也支持负数。 
- 如果比 1 小，会缩小图形，如果比 1 大会放大图形。默认值为 1。

> [!tip] 注意事项 
> - **画布初始情况下，是以左上角坐标为原点。如果参数为负实数，相当于以 x 或 y 轴作为对称轴镜像反转**。 
> 	- 例如，使用translate(0, canvas.height); scale(1,-1); 以 y 轴作为对称轴镜像反转。 
> - 默认情况下，canvas 的 1 个单位为 1 个像素。如果我们设置缩放因子是 0.5，1 个单位就变成对应 0.5 个像素，这样绘制出 来的形状就会是原先的一半。同理，设置为 2.0 时，1 个单位就对应变成了 2 像素，绘制的结果就是图形放大了 2 倍。


缩放案例实战 

- 第一步：先保存一下Canvas当前的状态，并确定缩放原点
- 第二步：在绘制图形前缩放画布 
- 第三步：开始绘制图形，并填充颜色

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758353387000d4osmr.png)


