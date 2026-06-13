# 四、精灵图(CSS Sprite)
## 4.1 认识CSS Sprite

* 是一种CSS图像合成技术，将各种小图片合并到一张图片上，**然后利用CSS的背景定位来显示对应的图片部分**
* 有人翻译为:CSS雪碧、CSS精灵

**使用CSs Sprite的好处**

* 减少网页的http请求数量，加快网页响应速度，减轻服务器压力
* 减小图片总大小
* 解决了图片命名的困扰，只需要针对一张集合的图片命名

**Sprite图片制作(雪碧图、精灵图)**

* 方法1:Photoshop,设计人员提供
* 方法2:https://www.toptal.com/developers/css/sprite-generator

## 4.2 CSS Sprite 的使用
**精灵图如何使用呢?**

* 精灵图的原理是通过只显示图片的很小一部分来展示的;
* 通常使用背景:
	* 设置对应元素的宽度和高度
	* 设置精灵图作为背景图片
	* 调整背景图片的位置来展示

获取精灵图的位置的网站： http://www.spritecow.com/

* 点击你需要的图标，下面就会给出代码。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/172310450200033ba46.png)


## 4.3 网易精灵图练习
```html
<style>
	i.icon_sprite {
		background-image: url(../imgs/music_sprite.png);
		background-repeat: no-repeat; 
		/* 图片不需要进行平铺 */
		display: inline-block;
	}
	i.logo {
		background-position: 0 -19px;
		width: 157px;
		height: 33px;
	}
	i.hot {
		background-position: -192px 0;
		width: 26px;
		height: 13px;
	}
</style>

<body>
    <div class="box" style="background-color: #333;">
        <i class="icon_sprite logo"></i>
        <i class="icon_sprite hot"></i>
    </div>
</body>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17231059560008k8gh5.png)

