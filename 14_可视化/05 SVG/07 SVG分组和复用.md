# 一、元素的组合(g)

**元素的组合：** 

- **`<g>` 元素是用来组合元素的容器。**
- 添加到g元素上的变换会应用到其所有的子元素上。 
- 添加到g元素的属性大部分会被其所有的子元素继承。 
- g元素也可以用来定义复杂的对象，之后**可以通过 `<use>` 元素来引用**它们

```html
<!-- 分组 -->
<svg width="400" height="400">
  <g  fill="transparent" stroke="black">
  <circle cx="50" cy="100" r="50"></circle>
  <circle cx="90" cy="100" r="50"></circle>
  <circle cx="130" cy="100" r="50"></circle>
  <circle cx="170" cy="100" r="50"></circle>
  </g>
</svg>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758617880000g2nuuj.png)

`<g>` 元素的属性（**该元素只包含全局属性**） 

- **核心属性：id** 
- 样式属性：class 、style 
- Presentation Attributes（**也可说是 CSS 属性，这些属性可写在CSS中，也可作为元素的属性用**）： 
	- cursor, display, fill, fill-opacity, opacity,…
	- stroke, stroke-dasharray, stroke-dashoffset, stroke-linecap, stroke-linejoin 
	- **更多表示属性**：https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/Presentation 
- 事件属性：onchange, onclick, ondblclick, ondrag… 
- 动画属性：transform 
- 更多：https://developer.mozilla.org/en-US/docs/Web/SVG/Element/g

# 二、图形元素的复用(defs)

SVG 是允许我们定义一些可复用元素的。 

- 即把**可复用的元素定义在 `<defs>` 元素里面，然后通过 `<use>` 元素来引用和显示**。 
- 这样可以增加 SVG 内容的易读性、复用性和利于无障碍开发。

`<defs>` 元素，定义可复用元素。

- 例如:定义基本图形、组合图形、渐变、滤镜、样式等等
- **在 `<defs>` 元素中定义的图形元素是不会直接显示的。**
- 可在视口任意地方用 `<use>` 来呈现在defs中定义的元素
- `<defs>` 元素没有专有属性，使用时通常也不需添加任何属性。
- **`<defs>` 里面定义的可以在外部 SVG 引入**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758621557000wf5gz3.png)

> [!tip] `<defs>` 定义的元素的坐标系参照哪个？**[[04 视口和视口框#一、视口-viewport|用户坐标系]]**

# 三、引入元素(use)

**`<use>` 元素从 SVG 文档中获取节点，并将获取到的节点复制到指定的地方。**

- `<use>` 等同于深度克隆DOM节点，克降到use元素所在的位置。
- 克隆的节点是不可见的，当给 `<use>` 元素应用CSS样式时须小心。因为克隆的 DOM 不能保证都会继承 `<use>` 元素上的CSS属性，但是CSS可继承的属性是会继承的。

**`<use>` 元素的属性**

- **href**： 需要复制元素/片段的 URL 或 ID（支持跨SVG引用）。默认值：无 
- ~~xlink:href：（SVG2.0已弃用）~~需要复制的元素/片段的 URL 或 ID 。默认值：无 
- **x / y** ：元素的 x / y 坐标（相对复制元素的位置）。 默认值：0 
- **width / height** ：元素的宽和高（<mark class="hltr-orange">在引入svg或symbol元素才起作用</mark>）。 默认值：0

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758621858000odfmen.png)
	
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758621869000huzvgw.png)


# 四、图形元素复用(symbols)

`<symbol>` 元素和 `<defs>` 元素类似，也是用于定义可复用元素，然后通过 `<use>` 元素来引用显示。

- 在 `<symbol>` 元素中定义的图形元素**默认也是不会显示在界面上**
- `<symbol>` 元素**常见的应用场景是用来定义各种小图标**，比如:icon、logo、徽章等

`<symbol>`元素的属性

- **viewBox:定义当前 `<symbol>` 的视图框**
- x/y:symbol元素的x/y坐标。;默认值:0
- width/height:symbol元素的宽度。默认值:0

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758624720000bouf2h.png)

`<symbol>` 和 `<defs>` 的区别

- **`<defs>` 元素没有专有属性，而 `<symbol>` 元素提供了更多的属性**
	- 比如:viewBox、preserveAspectRatio、x、y、width、 height等。
- `<symbol>` 元素有自己用户坐标系，可以用于制作SVG精灵图.
- `<symbol>` 元素定义的图形**增加了结构和语义性**，提高文档的可访问性。


> [!tip] SVG ICON文件-合并成SVG精灵图：https://www.zhangxinxu.com/sp/svgo

