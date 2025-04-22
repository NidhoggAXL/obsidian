# 一、认识固定定位
元素**脱离normal flow(脱离标准流、脱标)**
* 不占据位置
* 覆盖在标准流之上

可以通过**left、right、top、bottom**进行定位

* 定位**参照对象是视口(viewport)**
* 脱离标准流的时候，会有一个默认的位置（不用记得）
* 通过定位可以改变位置
* 当画布滚动时，固定不动
 
> [!tip] 画布和视口
> 一、视口（Viewport）
> * 文档的可视区域
> * 如右图**红框**所示
> 
> 二、画布（Canvsa）
> * 用于渲染文档的区域
> * 文档内容超出视口范围，可以通过滚动查看
> * 如右图**黑框**所示
> 
> 三、宽高对比
> **画布`>=`视口**
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17233619110003opxdb.png)

# 二、固定定位练习
```css
<style>
	.box {
		position: fixed;
		right: 20px;
		bottom: 20px;
	}
	.item {
		width: 80px;
		height: 40px;
		text-align: center;
		line-height: 40px;
		color: #fff;
		background-color:bisque;
		border-radius: 8px;
		/* 移动到上面是一个小手 */
		cursor: pointer;
	}
	.item:hover {
		background-color: red;
	}
	.top {
		margin-bottom: 6px;
	}
</style>

<div class="box">
	<div class="item top">顶部</div>
	<div class="item bottom">反馈</div>
</div>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723366319000klx642.png)

  



