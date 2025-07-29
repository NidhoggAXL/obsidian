# 一、认识盒子
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171506481200041yyy7.png)

事实上,我们可以把HTML每一个元素看出一个个的盒子:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715064963000v8on6m.png)

# 二、盒子模型
HTML中的每一个元素都可以看做是一个盒子，如右下图所示，可以具备这4个属性：

**内容(content)**

* 元素的内容width/height

**内边距(padding)**

* 元素和内容之间的间距

**边框(border)**

* 元素自己的边框

**外边距(margin)**

* 元素和其他元素之间的间距

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715065069000cv4342.png)


## 2.1 模型盒子的四边
因为盒子有四边,所以`margin/padding/border`都包`top/right/bottom/left`四个边:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715065348000e7y91x.png)

在浏览器的开发工具中：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17150655050001ngsx3.png)


# 三、内容-宽度和高度
 **设置内容是通过宽度和高度设置的:**
* 宽度设置: `width`
* 高度设置: `height`

> 注意: 对于**行内级非替换元素**来说,设置**宽高和高度**是无效的!


**另外我们还可以设置如下属性:**
* min-width:最小宽度，无论内容多少，宽度都大于或等于min-width
* max-width:最大宽度，无论内容多少，宽度都小于或等于max-width
* **移动端适配时,可以设置最大宽度和最小宽度**;

> [!tip] 使用场景
> 改变网页的大小的时候，里面的元素按照网页的大小，进行适配。网页的内容不会进行截断或者覆盖。

**下面两个属性不常用:**
* min-height:最小高度，无论内容多少，高度都大于或等于min-height
* max-height:最大高度，无论内容多少，高度都小于或等于max-height

## 3.1 宽度的默认值(auto)
块级元素：
* 没有进行 width 设置的时候是一个默认值
* 因为是块级元素所以独占一行（父元素的一行）

行内级元素：
* 行内级元素是不可以设置宽度和高度的，但是也有默认值（auto），由内容决定高度和宽度

行内级可替换元素：
* 例如 img 图片，可以设置高度和宽度，默认也是 auto 
* 浏览器会根据图片的大小自动设置渲染出在页面上面的大小

## 3.2 min-max-width
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171508529200000gz2k.png)

不管页面怎么调整，就只会显示出内容 `max-width` 的大小：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715085359000l4wkbg.png)

页面在缩小的时候也会有一个限制 `min-width` 最小宽度，当这个时候页面就不可以在进行缩小了：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715085430000792mht.png)

> 当页面在小的时候就会出现**滚动条（右边和下边都会出现）**来翻看内容，并不是缩小以后内容就看不了了：
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17150855500001k5t4l.png)

# 四、内边距-padding
**padding属性用于设置盒子的内边距,通常用于设置边框和内容之间的间距;**

**padding包括四个方向，所以有如下的取值:**
* `padding-top`:上内边距
* `padding-right`:右内边距
* `padding-bottom`:下内边距
* `padding-left`:左内边距

> [!tip] 注意
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715086174000vkutuo.png)
> 上下到边框的距离造成不是 padding ，是 line-height 造成的一个行边据（行据=（line-height）- 内容高度 。 行边距=行距/2）

## 4.1 padding的基本使用
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715086650000yvrs3u.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715086661000awbe4g.png)

## 4.2 padding缩写属性
**padding单独编写是一个缩写属性:**
* `padding-top、padding-right、padding-bottom、padding-left`的简写属性
* padding 缩写属性是**从零点钟方向开始**,沿着**顺时针转动**的,也就是上右下左;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715086953000qgz6jb.png)

## 4.3 padding的其他值
> padding 并非必须是四个值,也可以有其他值，

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17150871840002ns2ry.png)

## 4.4 padding的弊端
[[12 CSS的盒子模型（Box Model）#6.2.1 padding改变外元素内边距]]

# 五、边框-brder
**border用于设置盒子的边框:**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715087382000b8y6st.png)

**边框相对于content/padding/margin来说特殊一些:**

* 边框具备宽度`width`;
* 边框具备样式`style`;
* 边框具备颜色`color`;

## 5.1 边框宽度

* border-top-width, border-right-width, border-bottom-width, border-left-width
* border-width是上面4个属性的简写属性


## 5.2 边框颜色

* border-top-color, border-right-color、 border-bottom-color、 border-left-color
* border-color是上面4个属性的简写属性


## 5.3 边框样式
 * border-top-style、 border-right-style、 border-bottom-style、 border-left-style
 * border-style是上面4个属性的简写属性

边框的样式设置值：
* solid：坚硬的
* dashed：虚线
* dotted：有点的
* groove：凹槽,沟槽,边框看上去好象是雕刻在画布之内
* ridge：山脊,和grove相反，边框看上去好象是从画布中凸出来

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715089547000sp7rjo.png)

## 5.4 boder总缩写属性
**总缩写属性顺序可以交换，没有固定顺序**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715088520000pkqion.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715088559000uvvl4n.png)

**结果显示都是一样的：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715088577000x1q2vw.png)


**其中`coder-style`不可以省略，其他都可以省略**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715088604000cmwftu.png)

省略了就不会显示边框

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17150886110006mg74m.png)

**省略颜色，默认为黑色**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17150892570006z8s95.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17150892650001wjow4.png)


 **省略 width 宽度默认**
 
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171508945600030dw0e.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715089463000jzc0th.png)


## 5.5 圆角 boder-radius
**border-radius用于设置盒子的圆角**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715090328000wxxfq9.png)

**border-radius常见的值:**
* 数值: 通常用来设置小的圆角,比如6px;
* 百分比: 通常用来设置一定的弧度或者圆形;
	* 百分比是相对与boder的百分比（不用记，开发中很少用）

> border-radius 事实是一个缩写属性，开发中很少对每一个圆角进行设置
> 例如：`boder-top-left-radius:0`是对左上的角进行设置

> [!tip] boder-radius 到底是对什么设置的
> boder-radius 是对整个内容进行设置，并不只是对与有 boder 的内容进行设置的。而是对于整个元素进行设置。
> 可以理解为把设置圆角的内容隐藏了起来，但是隐藏起来的内容还是会占据空间。

### 5.5.1 设置具体的数值

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715091259000mcpubj.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17150912670007pgu9l.png)

### 5.5.2 百分比设置通常来做圆
* 百分比只要达到50就是圆了，超过设置是没有什么用的
* 开发中就设置50好了

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715091400000tflypv.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715091407000s6ki8e.png)


# 六、外边距-margin
**定义：** margin属性用于设置盒子的外边距,通常用于元素和元素之间的间距

**margin包括四个方向,所以有如下的取值:**
* margin-top:上内边距
* margin-right:右内边距
* margin-bottom:下内边距
* margin-left:左内边距

**margin单独编写是一个缩写属性:**
* `margin-top、margin-right、margin-bottom、margin-left`的简写属性
* margin缩写属性是从零点钟方向开始,沿着顺时针转动的,也就是上右下左

## 6.1 margin的其他值
margin也并非必须是四个值，也可以有其他值;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715171989000tfhjag.png)

## 6.2 padding 和 margin 的对比
改变盒子嵌套之间的距离：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715169850000dn9fqj.png)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715169855000f6c97r.png)

现在要改变盒子嵌套之间的距离：

### 6.2.1 padding改变外元素内边距

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17151700130001ns9ad.png)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17151700200006bp55m.png)


> 这样确实是让内容之间有了距离，但是有一个弊端，当`padding-left`**过大的时候会让父元素的撑起来**。
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17151701420004n5ra5.png)
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715170156000snw6sd.png)
> * 从这里可以看出 padding 的实际是在保证内容不变的情况下，向外扩张内边距的。


**使用`box-sing:boder-box;`来删除padding的弊端**

* `boder-box = 内容 + padding + boder`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715171020000wjohxd.png)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715171029000bna8ul.png)


### 6.2.2 margin改变内元素外边距
**margin 是不会撑开父元素：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17151712510001ly3b9.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715171266000yj22aa.png)

**如果也向把上边距产出距离**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715171527000l62l5e.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715171553000rcvyk8.png)

> [!tip] 特别注意
> * 这里为什么没有margin的传递，是因为我们这里设置了`display:inline-block`改变了div的快级元素，变成了行内积元素
> * 如果没有改变，那么是会存在margin的传递的
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715172730000nonb6f.png)
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17151727410008oiywk.png)

### 6.2.3 小结
**为什么会存在这个padding和margin的对比这些例子:**

> 这里**嵌套的都是快级元素**，本身就是独占一行，顶部都是页面显示的顶部了。
> 当对子元素设置`margin-top`的时候本身也是对父元素进行了设置

## 6.3 上下margin的传递
**margin-top传递**
* 如果块级元素的顶部线和父元素的顶部线重叠，那么这个块级元素的margin-top值会传递给父元素

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715173215000ar26r8.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715173234000whvb3s.png)

**margin-bottom传递**
* 如果**块级元素的底部线和父元素的底部线重合**，并且**父元素的高度是auto**，那么这个块级元素的margin-bottom值会传递给父元素

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715174006000fesehw.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715174018000vzmrva.png)

> 当然如果 .box 的height没有设置的话默认也是 auto 的。

### 6.3.1 如何防止出现传递问题?
* 给父元素设置`padding-top/padding-bottom`
* 给父元素设置`border`
* 触发BFC: 设置`overflow为auto`

### 6.3.2 小结（重点）
* margin一般是用来设置兄弟元素之间的间距
* padding一般是用来设置父子元素之间的间距
* 只有上下存在传递，左右没有传递

## 6.4 margin上下的折叠（collapse）
* 垂直方向上相邻的2个margin(margin-top、margin-bottom)有可能会合并为1个margin，这种现象叫做collapse(折叠)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17151746910005pebco.png)

> 事实上是没有50px，只有30px![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715174722000pv03it.png)

* 水平方向上的margin(margin-left、margin-right)永远不会collapse

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715174842000mnusgg.png)

> 要同一行显示，所以都设置属性`display:inline-block`
> 可以看出左右是不会存在折叠的
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715174901000w45ktm.png)


**折叠后最终值的计算规则**
* 两个值进行比较，取较大的值

**如何防止margin collapse?**
* 只设置其中一个元素的margin

### 6.4.1 其他折叠

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715175029000p8uw1w.png)



# 七、快级元素水平居中
## 7.1 使用inline-block

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17151757030008jirca.png)

> `test-align:center;`只对行内级元素有用，所以设置快级元素设置了`display:inline-block`
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715175798000k2aqb7.png)

## 7.2 使用margin
先看下面代码和结果：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715176361000087nrw.png)

> 结果：
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715176377000116oyf.png)

**为什么可以 margin 设置成这样就可以达到这样的效果呢？**

首先要知道不管是 HTML 还是 CSS 都是面对我们浏览器的

然后浏览器在对我们的内容进行渲染的时候，**块级元素**是必须占据父元素的整行的，但是我们需要显示的内容却小于父元素的宽度的，那么浏览器在渲染的时候就会把`父元素宽度-子元素宽度=多余的宽度`交给子元素的margin 

但是知道页面的前生是报纸，报纸是左对齐的，所以就把多余的宽度全部给了`margin-right`,块级元素就左对齐了。

**最后看文档：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715176948000k2czux.png)

> 上面的`margin:0 atuo`是一种 margin 的缩写，上下左右全部都进行了设置`（上下为0，左右为auto）`，如果不想上下也为0也是可以进行设置的。
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715177108000r4w5hw.png)
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715177117000wuisee.png)

那如何体现出来这个**块级元素独占父元素一行**呢？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715237634000w10rth.png)

> .box 是在 .content 父级元素里面进行水平居中。
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715237674000b0ol4i.png)

# 八、外轮廓-outline（了解）
**outline表示元素的外轮廓**
* **不占用空间**
* 默认显示在border的外面

**outline相关属性有**
* outline-width:外轮廓的宽度
* outline-style:取值跟border的样式一样，比如solid、dotted等
* outline-color: 外轮廓的颜色
* outline:outline-width、outline-style、outline-color的简写属性，跟border用法类似

## 8.1 基本使用
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715238695000fk2kcn.png)

> 因为`outline`属性不占据空间，所以超多浏览器左边就不会显示，并不会把 .box 撑起来。
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17152387690007uwa9o.png)


## 8.2 实际开发中
有些元素在默认的情况下浏览器会添加外轮廓的，但是认为是比较丑的，所以会把这个外轮廓设置为`none`来删除外轮廓。

例如：**a 元素和 input 元素就默认浏览器会添加外轮廓**（按 Tab ）键选中是会显示

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715239002000wb9k9j.png)

> 黑色的边框就是浏览器默认添加的外轮廓
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715239050000a4rppi.png)

那如何来删除这个外轮廓呢？就可以使用伪类元素或者使用属性选择器`outline:none;`
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715239348000gblpzq.png)

> 这样就不会在显示外轮廓了，但是伪类选择器和元素选择器选择后者，
> * 开发中，大多数元素都不需要这个外轮廓。
> * a **元素有好多中元素状态，这元素选择器中就把所有的状态都选择了**

[[09 伪类选择器#二、 动态伪类（dynamic pseude-classes）]]

# 九、盒子阴影 box-shadow
**box-shadow属性可以设置一个或者多个阴影**
* 每个阴影用`<shadow>`表示
* 多个阴影之间用逗号,隔开，从前到后叠加

> offfset - 偏移
> blur - 模糊

语法格式如下：
* 第1个`<length>`:offset-x,水平方向的偏移，正数往右偏移
* 第2个`<length>`:offset-y,垂直方向的偏移，正数往下偏移
* 第3个`<length>`:blur-radius,模糊半径
	* 可以省略，默认就是没有模糊
* 第4个`<length>`:spread-radius,延伸半径，向四个方向
* 第5个`<color>`:阴影的颜色，如果没有设置，就跟随color属性的颜色
	* 可以省略，默认黑色
* insert:外框阴影变成内框阴影
* 属性值是可以随机交换的，但是浏览器在识别渲染的时候，是从1~5依次进行识别的。
	* 有 模糊 才会有 延申 ，x 和 y 不能省略

**举例1**：只有偏移量

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715241081000jjlu1g.png)

> `x`和`y`轴的偏移量不可以省略任何一个
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715241182000zq6k32.png)

**举例2**：四个反向都要有阴影（要进行模糊和扩散）
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715241407000n6sa3o.png)

> 扩散后，上和左也就会有扩散
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17152414580009kya29.png)
> 通过观察扩散的结果可以知道，是在元素本身上面进行的扩散。

## 9.1 阴影盒子在线查看
做阴影设计的一个网站：
https://html-css-js.com/css/generator/box-shadow

> 注意这里的 opacity 实质是下面的 rgba


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715241880000nnnzze.png)


# 十、行内非替换元素的注意事项

padding、boder、margin-left/right 对于行内非替换元素都起作用。

margin-top、margin-bottom 对于行内非替换元素不起作用。

# 十一、CSS属性 box-sizing
box-sizing用来设置盒子模型中宽高的行为

content-box
* padding、border都布置在width、height外边

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715670232000je7hoo.png)


border-box
* padding、border都布置在width、height里边

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715670263000eww4nr.png)


**如果不加以设置的话，默认情况下是 content-box**

对比 content-box 和 boder-box

<div style="
  height: 500px; 
  overflow-y: auto;
  background: #fafafa;
">
  <img 
    src="https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715671878000z0h0b7.png" 
    style="
      width: 100%;
      display: block;
      border-radius: 4px;
    "
  />
</div>


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715671886000kxud6b.png)


# 十二、IE盒子模型
**W3C盒子模型**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715670728000s1kza8.png)

**IE盒子模型（IE8一下浏览器）**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715670763000s83z45.png)







