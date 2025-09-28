# 一、认识GSAP动画库

什么是GSAP 

- GSAP全称是（ GreenSock Animation Platform）GreenSock 动画平台。 
- GSAP 是一个强大的 JavaScript 动画库，可让开发人员轻松的制作各种复杂的动画。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758807381000nx64gm.png)

GSAP动画库的特点：

- 与Snap.svg不一样，GSAP无论是HTML 元素、还是SVG、或是Vue、React组件的动画，都可以满足你的需求。 
- GSAP的还**提供了一些插件**，可以用最少的代码创建令人震惊的动画，比如：ScrollTrigger插件和MorphSVG插件。 
	- https://greensock.com/scrolltrigger 
- GSAP 的核心是一个高速的属性操纵器，随着时间的推移，它可以极高的准确性更新值。**它比 jQuery 快 20 倍**！ 
- GSAP 使用起来非常灵活，在你想要动画的地方基本都可以使用，并且是零依赖。

GSAP官网：https://greensock.com/

# 二、GSAP初体验

GSAP初体验：移动SVG中的一个矩形 

- 引入 gsap.js 动画库（CDN，本地，npm）。 
- 调用 gsap.to 方法来执行 tween（补间/过度）动画。
	- 第一个参数是一个选择器，支持数组
	- 第二个参数是动画的配置，是一个对象

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758865612000dtglxu.png)


# 三、GSAP补间动画(Tween)

**GSAP的Tween动画有4中类型：** 

- gsap.from(targets | selector, vars) - 元素从from定义的状态过度到元素当前的状态。 
	- targets | selector ： 需动画的元素对象，支持字符串的选择器 
	- vars: 需过度动画的属性和GSAP扩展的duration、ease、transformOrigin、repeat、delay、yoyo、stagger、onComplete 等 
	- 官网gsap.form文档：https://greensock.com/docs/v3/GSAP/gsap.from() 
- gsap.to(targets | selector, vars) - 元素从当前的状态过度到to状态。 
- gsap.fromTo(targets | selector, fromVars， toVars) -元素从from定义状态过度到to定义的状态 
- gsap.set(targets | selector, vars) - 立即设置属性（无过度效果）。 
	- 本质上是一个 duration = 0 的 to 补间动画。
 
哪些属性可以设置动画？

- GSAP几乎可以为任何属性制作动画 
	- 包括 CSS 属性、元素属性、自定义对象属性。 
	- 甚至 CSS 变量和复杂的字符串。
	- 最常见的动画属性、变换和不透明度等。 
- GSAP还专门给CSS形变（transform）相关属性提供了简写，如下图所示：
	- 官网形变文档：https://greensock.com/get-started/#transformShorthand

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758866391000nd5y0k.png)

# 四、GSAP动画时间线(TimeLine)

什么是动画时间线（TimeLine）： 

- 时间线（TimeLine）是用来创建易于调整、有弹性的动画序列。 
- 当我们将补间添加到时间线（Timeline）时，默认情况下，它们会按照添加到时间轴的顺序一个接一个地播放。

TimeLine的使用步骤： 

- 第一步：通过gsap.timeline( vars ) 拿到时间线对象 
	- timeline文档： https://greensock.com/docs/v3/GSAP/Timeline 
- 第二步：调用时间线上的 Tween 动画方法，比如：form、to 等。

![gh|300](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758891341000uugrdj.png)

> [!tip] 
> - 支持链式调用：gsap.timelint.to().to()





