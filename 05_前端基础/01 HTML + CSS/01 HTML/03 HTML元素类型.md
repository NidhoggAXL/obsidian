# 一、HTML元素类型定义的思路（历史）

**HTML定义元素类型的思路**

* HTML元素有很多,比如 `h`元素 `p`元素 `div`元素 `span` 元素 `img`元素 `a`元素等等:
* 当我们把这个元素放到**页面上**时,这个元素**到底占据页面中一行多大的空间**呢?
	* 为什么我们这里只说一行呢? 因为**垂直方向的高度通常是内容决定的**
* 比如一个h1元素的标题,我们必然是希望它独占一行的,其他的内容不应该和我的标题放在一起;
* 比如一个p元素的段落,必然也应该独占一行,其他的内容不应该和我的段落放在一起;
* 而类似于`img/span/a`元素, 通常是**对内容的某一个细节的特殊描述, 没有必要独占一行,**


**为了区分哪些元素需要独占一行,哪些元素不需要独占一行,HTML将元素区分(<mark class="hltr-cyan">本质是通过CSS的</mark>)成了两类:**

* **块级元素(block-level elements)**:独占父元素的一行
* **行内级元素(inline-level elements)**:多个行内级元素可以在父元素的同一行中显示

# 二、通过CSS修改元素类型

**前面说过，事实上元素没有本质的区别:**

* div是块级元素，span是行内级元素;
* div之所以是块级元素仅仅是因为浏览器默认**设置了display属性**而已:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714912809000uzlfij.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714912831000apkcbr.png)

**本质还是CSS对元素进行修饰，不过这里的修饰不是自己添加的，而是 div 编写后被浏览器识别到，默认对 div 元素进行了修饰。**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17149129430002d65l8.png)

当然我们也可以对 div 的特性进行手动的 CSS 进行修改。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714913101000n5p4ow.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17149131110002fx62p.png)

这里也可以看出，行内级元素是由内容决定高度的，虽然设置了高度，但是设置的高度无效。

# 三、特殊元素类型行内级替换元素
## 3.1 img

**img 元素是 inline 也是 replace 行内级替换元素**

* 和其它行内级元素在同一行显示
* **可以设置宽度和高度**

> [!tip]
> 行内级非替换元素是不可以设置高度和宽度的，但是 img 虽然是行内级元素，但是同时也是可替换元素，所以可以设置高度和宽度。**img 不是行内级块元素。**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171491815400020wk99.png)

**修改 img 的行高和宽度：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714918221000rtfge7.png)

## 3.2 ::before 和 ::after

![[10 伪元素（pseudo-elements）#三、 before 和 after (常用)]]

> [!note] 如果要和行内级元素在一排显示就要使用`display:line-block`在进行设置


# 四、总结

1. 行内级(inline level)是不能设置高度和宽度的（行内级的高和宽是由内容决定的）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714917452000pz97fk.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714917486000nem03n.png)

> [!tip] 
>  - div 还是独占一行
>  - 行内级元素不可以修改高度和宽度（img-**行内级替换元素**除外）


