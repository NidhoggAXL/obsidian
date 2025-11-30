# 一、认识网页背景
在开发中,为了让网页更加美观,我们经常会设置各种各样的背景:

# 二、background-image

**background-image用于设置元素的背景图片** ^aed421

* 会盖在(不是覆盖)background-color的上面如果设置了多张图片


**设置的第一张图片将显示在最上面，其他图片按顺序层叠在下面**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716953248000oyhqwk.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716953262000rv3dyh.png)

> [!tip] 注意
> 如果设置了背景图片后，元素没有具体的宽高，背景图片是不会显示出来的


# 二、background-repeat
**background-repeat用于设置背景图片是否要平铺**

* 如果没有进行过图片设置的话，是默认平铺的

**常见的设值有**

* repeat:平铺
* no-repeat:不平铺
* repeat-x:只在水平方向平铺
* repeat-y:只在垂直平方向平铺


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17169534810001hu8ng.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17169534910003kwqvn.png)

背景平铺可以设置一些好看的图片

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716953629000sdmwal.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716953662000asyext.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716953671000oprc79.png)


# 三、background-size
**语法：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17169542220009sevs6.png)


**background-size用于设置背景图片的大小**

* auto:默认值,以背景图本身大小显示
* cover:缩放背景图，以完全覆盖铺满元素,可能背景图片部分看不见口 
* contain:缩放背景图，宽度或者高度铺满元素，**但是图片保持宽高比口**
* `<percentage>`:百分比，相对于背景区(background positioning area)
* length:具体的大小，比如100px

# 四、background-position
**background-position用于设置背景图片在水平、垂直方向上的具体位置**

* 可以设置具体的数值 比如 20px 30px(是可以设置为负值的);
* 水平方向还可以设值: left、center、right
* 垂直方向还可以设值: top、center、bottom
* 如果**只设置了1个方向，另一个方向默认是center**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716954495000f7642v.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716954449000zb6pa3.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17169544590004grirr.png)


**background-position 练习：**^background-positon

让图片随着网页的缩小而缩小，并且把图片的 center 重要的一直显示出来

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17169895720002t8zdt.png)

不进行网页缩小时：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716989594000csrqj9.png)


缩小时：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716989621000ncu97k.png)



# 五、background-attachment（了解）
**background-attachment决定背景图像的位置是在视口内固定，或者随着包含它的区块滚动**

attachment - 附件

* `scroll`:此关键属性值表示背景相对于元素本身固定，而不是随着它的内容滚动（默认）


* `local`:此关键属性值表示背景相对于元素的内容固定。如果一个元素拥有滚动机制，背景将会随着元素的内容滚动.
	* 比如文字内容的滚动的时候背景会和文字一起滚动



* `fixed`:此关键属性值表示背景相对于视口固定。即使一个元素拥有滚动机制，背景也不会随着元素的内容滚动。
	* 比如页面进行滚动的时候，背景图片不会进行滚动

# 六、background-缩写

**background是一系列背景相关属性的简写属性**

**常用格式是**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171699029000082tlxc.png)

`*`表示一个或者多个

`||`表示或，相连接的没有顺序之分

`[/]`表示里面内容可以省略，如果不省略的或后面就要加`/属性`

* `background-size`可以省略，如果不省略，`/background-size`必须紧跟在`background-position`的后面
* 其他属性也都可以省略，而且顺序任意


# 七、background-image和img对比
**利用background-image和img都能够实现显示图片的需求，在开发中该如何选择?**

|              |     img      | background-image |
| :----------: | :----------: | :--------------: |
|      性质      |   HTML 元素    |      CSS 样式      |
|   图片是否占用空间   |      是       |        否         |
| 浏览器右键之间查看地址  |      是       |        否         |
| 支持CSS Sprite |      否       |        是         |
| 更有可能被搜索引擎收录  | 是（结合 alt 属性） |        否         |

> [!tip] 总结
> `img`，作为网页内容的重要组成部分，比如广告图片、LOGO图片、文章配图、产品图片
> `background-image`，可有可无。有，能让网页更加美观。无，也不影响用户获取完整的网页内容信息


