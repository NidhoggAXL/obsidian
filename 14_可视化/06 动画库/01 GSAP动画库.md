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

