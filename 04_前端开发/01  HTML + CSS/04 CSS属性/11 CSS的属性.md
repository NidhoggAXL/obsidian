# 一、CSS属性继承
CSS的某些属性具有继承性(Inherited):
* 如果一个属性**具备继承性**,那么在该元素上**设置后**,它的**所有后代元素都可以继承这个属性。**
* 当然,如果**后代元素自己有设置该属性**,那么**优先使用后代元素自己的属性**(不管继承过来的属性权重多高)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714900577000cno1c2.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714900591000j1mt3f.png)

> div 元素具有继承性，后代 h1 和 p 和 h2 和 span 都继承了div 的属性

## 1.1 那些属性可以继承
**如何知道一个属性是否具有继承性呢?**

* 常见的`font-size/font-family/font-weight/line-height/color/text-align`都具有继承性
* 这些**不用刻意去记,用的多自然就记住了**
* 可以通过查阅文档来查询继承性
* 通过浏览器的检查可以看到

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714904744000uve71t.png)


> **一般**和文本相关的属性是可以继承的

> [!tip] 注意（了解）
> 继承过来的是计算值，不是设置值。
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171490397500001kan4.png)
> * em 是相对于父元素的倍数，如果没有父元素，那么就是浏览器当作为父元素
> * 这里浏览器默认是字体是 16px ， 那个 2em （计算值）= 32px，那么 p 元素继承的就是 32px ，而不是让这里的 em 以 16px（设置值）来做单位（1em = 32px），而是计算值 32px（1em=16）。



## 1.2 强制继承（了解）
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17149049650008l0vnl.png)

border 是不可以继承的，但是 p 元素里面使用了 `boder:inherit`强制继承了 boder 的属性。


# 二、CSS属性层叠
CSS的翻译是层叠样式表，什么是**层叠**呢?
* 对于一个元素来说**,相同一个属性**我们可以**通过不同的选择器给它进行多次设置**
* 那么属性会**被一层层覆盖上去**,
* 但是最终**只有一个会生效**:

**那么多个样式属性覆盖上去,哪一个会生效呢?**
* 判断一: 选择器的权重,权重大的生效, 根据权重可以判断出优先级（权重是可以进行累加的-同一个属性在不同的选择器中都设置成一样的）
* 判断二: 先后顺序, 权重相同时,后面设置的生效;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714906408000jwdpta.png)


## 2.1 选择器的权重
按照经验，为了方便比较CSS属性的优先级，可以给CSS属性所处的环境定义一个权值(权重)
* !important:  10000 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714905790000w3h9uc.png)

* 内联样式:  1000 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714905824000t6jv3o.png)

* id选择器:  100

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714905848000uijkvq.png)

* 类选择器、属性选择器、伪类:  10 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17149058750000t5x4g.png)

* 元素选择器、伪元素:  1  

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714905919000dxcozh.png)

* 通配符:  0 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714905935000sqxock.png)

> [!tip] 权重是可以进行累加的
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17149060980005r1sz9.png)


# 三、CSS属性-display
CSS中有个display属性，能修改元素的显示类型，有4个常用值
* block:让元素显示为块级元素
* inline:让元素显示为行内级元素
* inline-block:让元素同时具备行内级、块级元素的特征
* none:隐藏元素

## 3.1 block 和 inline 
![[03 HTML元素类型#二、通过CSS修改元素类型]]


## 3.2 inline-block
这个属性设置出来的原因：
> 当一个块级元素想变成一个行内级元素并设置高度和宽度的时候`display: inline`。
> 但是行内级元素又不可以设置高度和宽度
> 这个时候就产生了 `inline-block`行内块级元素。

**块级元素变成行内级元素，行内级元素不可以设置高度和宽度：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714919479000341j5a.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714919495000chz156.png)


使用`inline-block`属性：
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714919337000a0kdw3.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714919353000abv1nu.png)


## 3.3 总结
**block元素:**
* 独占父元素的一行
* 可以随意设置宽高
* 高度默认由内容决定

**inline:**
* 跟其他行内级元素在同一行显示;
* 不可以随意设置宽高;
* 高度和宽度都由内容决定

**inline-block元素:**
* 跟其他行内级元素在同一行显示
* 可以随意设置宽高
* 可以这样理解
	* 对外来说，它是一个行内级元素
	* 对内来说，它是一个块级元素

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714920246000v4cnt4.png)

# 四、元素隐藏方法 
**方法-: display设置为none**
* 元素不显示出来,并且也不占据位置,**不占据任何空间(和不存在一样)**;

**方法二: visibility(可见的)设置为hidden(隐藏的)**
* 设置为hidden,虽然元素不可见,但是会占据元素应该**占据的空间**:
* 默认为visible, **元素是可见的**;

**方法三:rgba设置颜色，将a的值设置为0**
* rgba的a设置的是alpha值,可以设置透明度, **不影响子元素**,
* **会占据位置**

**rgba：**
* r - red - 红色 0~255
* g - green - 绿色 0~255
* b - blue - 蓝色 0~255
* a - alpha - 0(透明)~1(不透明)

**方法四: opacity设置透明度,设置为0**
* 设置整个元素的透明度,会**影响所有的子元素**;
* **会占据位置**

## 4.1 display设置为none
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714972402000tjcw2u.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714972460000y9wiw9.png)


> div 被隐藏了，没有显示也不占据位置


## 4.2 visibility(可见的)设置为hidden(隐藏的)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714972582000bn1mlf.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17149726070003zi2ly.png)

> div虽然也被隐藏了，但是还是会占据位置

## 4.3 RGBA：
**a - alpha 0(透明)~1(不透明)**

**设置为半透明：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171497420000051yche.png)


> * a 如果是使用 16进制的写法在有些浏览器上面不支持
> * 使用rgba隐藏元素还是会占据空间

**也可以把背景设置成透明的：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171506203200098wbhx.png)

**这样背景是透明的，但是文本并没有透明：**

 > * 其实在没有设置背景颜色的时候 `background-color` 是默认为 `transparent(透明) `
 > 	* 只是会设置自己的透明度，并不会对子元素有影响
 > 	![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715062430000be71we.png)![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17150624600005koqk4.png)
 > 	**img 并没有设置透明**


## 4.4 opactiy
opactiy：设置透明度，并且会携带所有的子元素都有一定的透明度。
* 这里的 opactiy 是没有继承性的，但是它设置透明不是利用继承来设置透明的，而是把整个包括子元素设置为透明的。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715062620000g3wklz.png)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715062631000dub8n9.png)


> **img 是具有透明度的**


# 五、CSS属性-overflow
**overflow用于控制内容溢出时的行为：**

* `visible`:溢出的内容照样可见
* `hidden`:溢出的内容直接裁剪
* `scroll`:溢出的内容被裁剪，但可以通过滚动机制查看
	* 会一直显示滚动条区域，**滚动条区域占用的空间属于width、height**
* `auto`:自动根据内容是否溢出来决定是否提供滚动机制

> 文本默认是`overflow:visible`的。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715063604000mb5qqp.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715063616000i4x6mn.png)

# 六、CSS样式不生效技巧
**为何有时候编写的CSS属性不好使，有可能是因为**
* 选择器的优先级太低
* 选择器没选中对应的元素
* CSS属性的使用形式不对
	元素不支持此CSS属性，比如span默认是不支持width和height的
	浏览器不支持此CSS属性，比如旧版本的浏览器不支持一些css module3的某些属性
	被同类型的CSS属性覆盖，比如font覆盖font-size


> [!tip] 建议
> 充分利用浏览器的开发者工具进行调试(增加、修改样式)、查错





