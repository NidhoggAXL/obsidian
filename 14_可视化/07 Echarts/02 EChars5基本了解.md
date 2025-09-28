# 一、初体验ECharts

集成 Echarts 的常见方式： 

1. 通过 npm 获取 echarts： 
	- npm install echarts --save 
2. 通过 jsDelivr 等 CDN 引入 

初体验Echarts（容器必须设高度）


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758956937000kd0xon.png)


```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>ECharts</title>
    <!-- 引入刚刚下载的 ECharts 文件 -->
    <script src="../libs//echarts-5.3.3.js"></script>
  </head>
  <body>
    <!-- 为 ECharts 准备一个定义了宽高的 DOM -->
    <div id="main" style="width: 600px;height:400px;"></div>
    <script type="text/javascript">
      // 基于准备好的dom，初始化echarts实例
      var myChart = echarts.init(document.getElementById('main'));

      // 指定图表的配置项和数据
      var option = {
        xAxis: {
          data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子']
        },
        yAxis: {},
        series: [
          {
            name: '销量',
            type: 'bar',
            data: [5, 20, 36, 10, 10, 20]
          }
        ]
      };

      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
    </script>
  </body>
</html>
```

# 二、ECharts渲染原理

浏览器端的图表库大多会选择 [[01 邂逅SVG|SVG]] 或者 [[01 邂逅Canvas|Canvas]] 进行渲染。 

**ECharts 最开始时一直都是使用 Canvas 绘制图表**。直到 ECharts v4.0 版本，才发布支持 SVG 渲染器。 

SVG 和 Canvas 这两种使用方式在技术上是有很大的差异的，EChart能够做到同时支持，主要归功于 ECharts 底层 库 **ZRender** 的抽象和实现。

**ZRender 是二维轻量级的绘图引擎，它提供 Canvas、SVG、VML 等多种渲染方式**。 

因此，Echarts 可以轻松的互换SVG 渲染器 和 Canvas 渲染器。切换渲染器只须在初始化图表时设置 renderer 参数 为canvas 或svg即可。

默认使用Canvas渲染：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758957223000yu9eog.png)

修改为使用 SVG 渲染：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758957346000xf5rhw.png)


