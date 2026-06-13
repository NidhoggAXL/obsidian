# 一、行盒

行盒：inline box

作用：将**当前行**里面的**所有的内容包裹**起来

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725447163000ys5w3f.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725447094000uhzxdn.png)

其实每一行都是有一个行盒子的，只是这个盒子是一个隐藏的盒子，我们就叫这个盒子为行盒。

> [!tip] 重点理解
> **行高为什么可以撑起div的高度?**
> * 这是因为line boxes的存在，并且line-boxes有一个特性，包裹每行的inline level
> * 而其中的文字是有行高的，必须将整个行高包裹进去，才算包裹这个line-level
> 
> 元素在没有设置高度的时候，会显示出高度的原因我们会说是内容把高度撑起来了，其实本质是总的行高`line-height`把高度撑起来啦。


看一下下面这个例子：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725448458000ol0vbd.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725448478000lfbu28.png)


这里可以看出来包含块和里面的图片设置了同样的高度，这样把图片完全包含了进去，但是图片后面的文字内容却感觉是超出了包含快这是为什么呢？


> 这里面就是体现了行盒（行盒是把当前行内的所有内容都包裹起来的），
> 其中文字的内容有行高的关系，图片又与文字内容基线对齐，**这样看来其实行盒比包含快都要大一点的。**


# 二、bertical-align

**通过上面的行盒在进一步思考分类？**

**情况一**:只有文字时，line boxes如何包裹内容?(注意:红色是包裹的div，下面也都一样)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725449799000kvhfff.png)

**情况二**:有图片，有文字时，line-boxes如何包裹内容?

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725449816000uhoftg.png)

**情况三**:有图片，有文字，有inline-block(比图片要大)如何包裹内容?

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725449834000e5y3hs.png)

**情况四**:有图片，有文字，有inline-block(比图片要大)而且设置了margin-bottom，如何包裹内容?

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/172544987000028ni9a.png)

**情况五**:有图片、文字、inline-block(比图片要大)而且设置了margin-bottom并且有文字，如何包裹内容?

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725449968000q30au7.png)

> 当一个inline-box中有文本时,它的基线不再是底部基线变成**最后一行文本的基线**

**情况六**：两个块级元素里面都包裹了图片，那么两块级元素之间会有间隙吗？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725452201000qjneuv.png)

发现还是会有的，那么如果对第一个块级元素设置一个和图片同样的高度呢？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725452257000qv6omo.png)

会发现两个图片的接触的地方就没有间隙了。

> [!tip] 重点
> 从情况六可以看出其实行盒（line box）是不受包裹行内级元素的包含块影响的，本身就是一个独立。
> * 如果没有对包含块设置高度的话，那么 line box 是会占据高度的
> * 如果对包含块设置了高度，那么 line box 不会占据高度，但是还是会遵守包含行内级元素，并默认进行基线对齐。

## 2.1 vertical-align的baseline

**baseline（基线）到底是谁呢？**

* 文本的baseline是字母x的下方
* Inline-block默认的baseline是margin-bottom的底部(没有，就是盒子的底部)
* Inline-block有文本时，baseline是最后一行文本的x的下方


## 2.2 vertical-align的其他值

**baseline(默认值)**:基线对齐(你得先明白什么是基线)

**top**:把行内级盒子的顶部跟line boxes顶部对齐

**middle**:行内级盒子的中心点与父盒基线加上x-height一半的线对齐 

* 但是我们这里还要知道一点，文字在浏览器渲染的时候是默认会文字下沉一点。

**bottom**:把行内级盒子的底部跟line box底部对齐

`<percentage>`:把行内级盒子提升或者下降一段距离`(距离相对于line-height计算\元素高度)`，0%意味着同baseline-样

`<length>`:把行内级盒子提升或者下降一段距离，0cm意味着同baseline一样

**解决图片下边缘的间隙方法**

* 方法-:设置成top/middle/bottom
* 方法二:将图片设置为block元素;

