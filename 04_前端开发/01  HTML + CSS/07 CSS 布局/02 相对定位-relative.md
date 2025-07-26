# 一、认识相对定位
**元素依旧按照normal flow布局**

可以通过left、right、top、bottom进行定位

* 定位参照对象是元素自己原来的位置

left、right、top、bottom用来设置元素的具体位置，对元素的作用如下图所示

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723207151000ihmjbi.png)

**相对定位的应用场景**

* 在不影响其他元素位置的前提下，对当前元素位置进行**微调**

# 二、相对定位-relative 练习

**完成次方的运算**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17232080470001ycvn6.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723208058000eluojm.png)


**图片的一直居中显示（不随窗口的改变而改变聚焦的位置）**

* 使用[[13 CSS设置背景#^background-positon|background-positon]]也可以完成

```html
<style>
	body {
		padding: 0;
		margin: 0;
	}
	.box {
		background-color: red;
		height: 489px;
		/* 让窗口不要出现滚动条 */
		overflow: hidden;
	}
	.box img {
		position: relative;
		/* left 设置为图片的一半 */
		left: -960px;
		/* 也可以如下设置 */
		/* transform: translate(-50%); */
		/* tanslate的百分比是相较于自己 */

		/* 向右移动父级元素（div）的一半 */
		margin-left: 50%;
	}
</style>

<body>
    <div class="box">
        <img src="../imgs/mhxy.jpg" alt="">
    </div>
</body>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723210660000aamkv5.png)

思路分析：

![[相对定位]]

这个过程的目的就是要保证 img 和 div 的中线始终的保持一致。
先使用 left 让 img 的中线到 div 的开头。
在让 img 的中线始终在 div 宽度的一半。

> 看似是 img 左边的调整，实质是为了调整中线。

> [!tip] 那如何在这两种方案中选择呢？
> 在网页中如果这个图片是整个网站中重要的组成部分，最好用相对定位来完成
> 因为背景图片在网页中是可有可无的东西，重要的东西还是使用 img 用相对定位来完成。






