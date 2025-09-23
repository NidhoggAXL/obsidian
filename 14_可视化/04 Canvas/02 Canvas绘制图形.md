# 一、初体验Canvas

使用Canvas的注意事项： 

- `<canvas>` 和 `<img>`  元素很相像，唯一的不同就是它并**没有 src 和 alt 属性**。
- `<canvas>` 标签只有两个属性——width和height( **单位默认为px )**。当没有设置宽度和高度时，canvas 会**初始化宽为 300px 和高为 150px**。 
- 与 `<img>`  元素不同，`<canvas>` 元素**必须需要结束标签 (`</canvas>`)**。如结束标签不存在，则文档其余部分会被认为是**替代内容**，将不会显示出来。 
- 测试 **canvas.getContext() 方法的存在，可以检查浏览器是否支持Canvas**。

初体验Canvas 

- 1. Canvas通用模板 

```html
<style>
  body {
    margin: 0;
    padding: 0;
  }
  .box {
    background-color: rgba(255, 0, 0, .2);
  }
</style>

<body>
  <canvas class="box">
    您的浏览器不支持canvas,请升级浏览器!
  </canvas>

  <script>
    window.onload = function () {
      const canvasEl = document.querySelector('.box')
      console.log(canvasEl)
    }
  </script>
</body>
```

- 2. Canvas绘制正方形

```html
<script>
  window.onload = function () {
    const canvasEl = document.querySelector('.box') 
    let ctx = canvasEl.getContext('2d') // 获取canvas的2D绘图上下文
    ctx.fillRect(0, 0, 100, 100) // 在canvas上绘制一个100x100像素的矩形，填充位置从(0,0)开始
  }
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175820226600034a599.png)


# 二、Canvas Grid和坐标空间

Canvas Grid 或 坐标空间 

- 假如，HTML 模板中有个宽 150px, 高 150px 的 `<canvas>` 元素。**`<canvas>`元素默认被网格所覆盖。** 
- 通常来说网格中的一个单元相当于 canvas 元素中的一像素。 
- 该网格的原点位于坐标 (0,0) 的左上角。**所有元素都相对于该原点放置**。

**网格也可以理解为坐标空间（坐标系）**，坐标原点位于canvas元素的左上角，被称为初始坐标系 

- 如下图中蓝色正方形，左上角的坐标为距离左边 x 像素，距离上边y 像素，坐标为（x, y） 


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758202560000vyzonp.png)



网格或坐标空间是可以变换的，后面会讲如何将原点转换到不同的位置，旋转网格甚至缩放它。 

> [!warning] 注意：移动了原点后，默认所有后续变换都将基于新坐标系的变换。

# 三、绘制矩形(Rectangle)

Canvas支持两种方式来绘制矩形：**矩形方法** 和 **[[03 Canvas样式和颜色#五、绘制矩形(Rectangle)|路径方法]]**。 

- 路径是通过不同颜色和宽度的线段或曲线相连形成的不同形状的点的集合。 
- 除了矩形，其他的图形都是通过一条或者多条路径组合而成的。 
- 通常我们会通过众多的路径来绘制复杂的图形。

Canvas 绘图的**矩形方法**： 

- **fillRect(x, y, width, height)**： 绘制一个填充的矩形 
- **strokeRect(x, y, width, height)**： 绘制一个矩形的边框 
- **clearRect(x, y, width, height)**： 清除指定矩形区域，让清除部分完全透明。

方法参数： 

- 上面的方法都包含了相同的参数。 
- x 与 y 指定了在canvas画布上所绘制矩形的左上角（相对于原点）的坐标（不支持 undefined ）。 
- width 和 height 设置矩形的尺寸。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17582478950005u4pwr.png)
