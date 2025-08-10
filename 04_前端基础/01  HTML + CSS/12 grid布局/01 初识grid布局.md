# 一、认识grid布局
目前对于界面布局我们已经学习了多种方式:定位、浮动、fex布局:

flex布局相对于前面的布局来说更加的强大，并且目前对于我们的需求都是可以很好的完成。

* 但是flex是一个一维的布局方案(one-dimensionallayout)
* 它主要的布局是在主轴(main axis)上进行操作，当然也提供了一些交叉轴(cross axis)属性;

CSS为了进一步增强自己的布局能力，提供了grid布局:

* css Grid Layout(又名“Grid”或“css Grid”)是一种基于二维的布局系统(two-dimensionallayout);
* 它更加强大，同时也更加复杂:

> 目前公司生产环境的项目基本都是使用fiex布局为主，因为它兼容性比flex布局差一些，所以grid布局暂时作为了解即可。

# 二、grid布局的重要概念
Grid Container

* 元素设置display为grid的盒子。

Grid ltem,单元格称之为grid cell

* grid container的直接子项(必须是直接子代)

Grid Line

* 构成网格结构的分割线。
* 它们可以是垂直的(“列网格线”)或水平的(“行网格线”)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17267336270006apbgh.png)

Grid Track

* 两条相邻网格线之间的空间;
* 你可以看成是网格的行或者列;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1726733646000u03qka.png)


Grid Area

* 由四条网格线包围的总空间。
* 一个网格区域可以由任意数量的网格单元组成。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1726733663000bn5cfm.png)


# 三、grid布局常见的属性

**grid container常见属性**

口 display
grid-template-columns
grid-template-rows
grid-template-areas
grid-template
口 grid-column-gap
grid-row-gap
grid-gap
口justify-items
口 align-items
place-items
口 justify-content
align-content
place-content
口 grid-auto-columns
grid-auto-rows
grid-auto-flow
0 grid


**grid item常见属性**

日 grid-column-start
口 grid-column-end
口 grid-row-start
口 grid-row-end
日 grid-column
ロ grid-row
ロ grid-area
口justify-self
口 align-self
口 place-self


学习：https://css-tricks.com/snippets/css/complete-quide-grid/
