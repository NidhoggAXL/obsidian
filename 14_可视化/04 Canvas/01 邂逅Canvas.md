# 一、认识Canvas

什么是Canvas 

- Canvas 最初由Apple于2004 年引入，用于Mac OS X WebKit组件，为仪表板小部件和Safari浏览器等应用程序提供支持。 后来，它被Gecko内核的浏览器（尤其是Mozilla Firefox），Opera和Chrome实现，并被网页超文本应用技术工作小组提议为下一代的网络技术的**标准元素（HTML5新增元素）**。 
- C**anvas提供了非常多的JavaScript绘图API（比如：绘制路径、矩形、圆、文本和图像等方法），与 `<canvas`元素可以绘制 各种2D图形。** 
- Canvas API 主要聚焦于 2D 图形。当然也可以使用 `<canvas>` 元素对象的 WebGL API 来绘制 2D 和 3D 图形。

Canvas的应用场景 

- 可以用于动画、游戏画面、数据可视化、图片编辑以及实时视频处理等方面。

Canvas 浏览器兼容性

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17582003290000tbt8v.png)

# 二、Canvas优缺点

**Canvas 优点：** 

- Canvas提供的功能更原始，**适合像素处理，动态渲染和数据量大的绘制**，如：图片编辑、热力图、<mark class="hltr-orange">炫光尾迹特效</mark>等。 
- Canvas非常适合图像密集型的**游戏开发**，适合频繁重绘许多的对象。 
- Canvas能够以 .png 或 .jpg 格式保存结果图像，**适合对图片进行像素级的处理**。

**Canvas 缺点：** 

- 在移动端可以能会因为Canvas数量多，而导致内存**占用超出了手机的承受能力**，导致浏览器崩溃。 
- Canvas 绘图**只能通过JavaScript脚本操作**（all in js）。
- Canvas 是由一个个**像素点构成的图形**，放大会使图形变得颗粒状和像素化，导致模糊。

