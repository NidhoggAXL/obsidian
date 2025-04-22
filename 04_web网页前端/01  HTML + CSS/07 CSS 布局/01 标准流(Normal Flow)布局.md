# 一、什么是标准流
 默认情况下，元素都是按照normal flow(标准流、常规流、正常流、文档流【document flow】)进行排布

* 从左到右、从上到下按顺序摆放好
* 默认情况下，互相之间不存在层叠现象

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723188282000ec6rih.png)

# 二、margin-padding位置调整
**在标准流中，可以使用margin、padding对元素进行定位**

* 其中margin还可以设置负数

**比较明显的缺点是**

* 设置一个元素的margin或者padding，通常会影响到标准流中其他元素的定位效果
* **不便于实现元素层看的效果**

**如果我们希望一个元素可以跳出标准流,单独的对某个元素进行定位呢?**

* 我们可以通过position（位置）属性来进行设置;
* `position:fixed` fixed-固定

# 三、认识元素定位
**定位允许您从正常的文档流布局中取出元素，并使它们具有不同的行为:**

* 例如放在另一个元素的上面:
* 或者始终保持在浏览器视窗内的同一位置;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723205919000gju4av.png)

# 四、认识position
利用position可以对元素进行定位，常用取值有5个:

| static | relative | absolute | sticky | fixed |
| ------ | -------- | -------- | ------ | ----- |
| 静态     | 相对       | 绝对       | 固定     | 粘性    |

默认值：static（静态定位）

**使用下面的值,可以让元素变成 定位元素(positioned element)**

* relative:相对定位
* absolute:绝对定位
* fixed:固定定位
* sticky:粘性定位

# 五、静态定位-static
**position属性的默认值**

* 元素按照normal flow布局
* left、right、top、bottom没有任何作用



