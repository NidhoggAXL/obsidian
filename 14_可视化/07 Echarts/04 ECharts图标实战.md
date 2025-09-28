# 一、柱形图

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1759042851000bblo2b.png)

![[00 Echarts5基础学习路线#1.柱形图]]

# 二、折线图

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17590453210000283b4.png)

![[00 Echarts5基础学习路线#2.折线图]]

# 三、拼图

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17590453630004q0stt.png)

![[00 Echarts5基础学习路线#3.饼图]]


# 三、地图

## 3.1 地图绘制

ECharts 可以使用 GeoJSON 格式的数据作为地图的轮廓，可以获取第三方的 GeoJSON 数据注册到 ECharts 中： 

- https://github.com/echarts-maps/echarts-china-cities-js/tree/master/js/shape-with-internal-borders 
- https://datav.aliyun.com/portal/school/atlas/area_selector

### ECharts绘制地图步骤（方式一）： 

1. 拿到GeoJSON数据 
2. 注册对应的地图的GeoJSON数据（调用setOption前注册） 
3. **配置geo选项**。

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1759047131000hb20sx.png)


![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1759047098000w8wp7l.png)


当然我们也可以不通过别人的 js 代码来进行 echarts.registreMap 的注册，而是自己注册，并且选择注册名

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1759047543000bgydla.png)


### ECharts绘制地图步骤（方式二）： 

1. 拿到GeoJSON数据 
2. 注册对应的地图的GeoJSON数据（调用setOption前注册） 
3. **配置map series**。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17590468460002ruul4.png)


## 3.2 两种方式的区别

geo地理坐标系组件：

- **会生成一个 geo 地理坐标系组件** 
- 地理坐标系组件用于地图的绘制 
- 支持在地理坐标系上绘制 **散点图**，**线集**。 
- 该坐标系可以共其它系列复用 
	- **注意**：其他系列在复用该地理坐标系时，series的itemStyle等样式将不起作用

map series：

- 默认情况下，map series 会自己生成**内部专用的 geo 地理坐标系组件** 
- 地理坐标系组件用于地图的绘制 
- 地图主要<mark class="hltr-orange">用于地理区域数据的可视化，配合data使用 </mark>
- 配合 **visualMap** 组件用于展示不同区域的人口分布密度等数据


## 3.3 地图着色

地图着色，可以通过 itemStyle 属性中的 areaColor 和 borderColor 属性。 

- areaColor ：地图区域的颜色； 
- borderColor：图形（边界）的描边颜色。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1759048987000rulm96.png)


## 3.4 地图数据可视化

给地图添加数据，并可视化展示 

- 添加一个map series 
- 配置地图样式 
- **添加地图所需的数据** 
- 添加 visualMap 视觉映射

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1759049624000sg3dj2.png)

```json
var option = {
	视觉数据映射
	visualMap: [
	  {
		// type: "continuous", // 连续型视觉映射组件 (默认)
		// type: "piecewise", // 分段型视觉映射组件
		left: "20%",
		seriesIndex: [0], // 指定取哪个系列的数据
		// 定义 在选中范围中 的视觉元素, 对象类型。
		inRange: {
		  color: ["#04387b", "#467bc0"], 
		  // 映射组件和地图的颜色(一般和地图色相近)
		},
	  },
	],          
}
```


## 3.5 地图涟漪特效散点图

给地图添加涟漪特效的散点图数据，并可视化展示 

- 添加一个**effectScatter series** 
- 指定使用的地理坐标系 
- **添加地图所需的数据** 
- 修改标记的大小和样式 
- 修改默认的tooltip提示

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17590552580001dz61l.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1759055289000fyj5j5.png)




