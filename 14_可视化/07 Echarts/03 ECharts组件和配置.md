# 一、认识option配置项(组件)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758974092000uhd5lj.png)


backgroundColor ：设置直角坐标系内绘图区域的背景 

grid 选项 ：直角坐标系内绘图区域  

yAxis 选项 ：直角坐标系 grid 中的 y 轴  

xAxis 选项 ：直角坐标系 grid 中的 x 轴  

title ：图表的标题  

legend：图例，展现了不同系列的标记、颜色和名字  

tooltip：提示框 

toolbox：工具栏，提供操作图表的工具  

series：系列，配置系列图表的类型和图形信息数据  

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758974104000h8ui4w.png)


visualMap：视觉映射，可以将数据值映射到图形的形状、大小、颜色等  

geo：地理坐标系组件。用于地图的绘制，支持在地理坐标系上绘制散点图，线集。

# 二、Grid网格配置(组件)
grid 选项 ：直角坐标系内绘图区域 

- show : 是否显示直角坐标系网格。 boolean类型。
- left、right、top、bottom： grid 组件离容器左右上下的距离。 string | number类型。 
- **containLabel**：grid 区域是否包含坐标轴的**刻度标签**。 boolean类型。 
- backgroundColor： Color类型，网格背景色，默认透明。
- 更多属性：https://echarts.apache.org/zh/option.html#grid

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758975210000fbpp6v.png)

> [!note] 为什么top和left都为0了，left还是会显示左边的刻度线？
> containLabel： true 保证有刻度的可以显示，left有刻度，而top没有刻度

# 三、坐标系配置(组件)

xAxis 选项 ：直角坐标系 grid 中的 x 轴 

- show 是否显示 x 轴。 : boolean 类型。 
- name：坐标轴名称。 
- type ： 坐标轴类型。 string 类型。 
	- value 数值轴，适用于连续数据。 
	- **category 类目轴**，适用于离散的类目数据。类目数据可来源 xAxis.data 、series.data 或 dataset.source 之一 。 
- **data：类目数据，在类目轴（type: 'category'）中有效。 array 类型**
- axisLine： 坐标轴**轴线**相关设置。 object 类型 
- axisTick：坐标轴**刻度**相关设置。 object 类型 
- axisLabel：坐标轴**刻度标签**的相关设置。 object 类型 
- splitLine：坐标轴在 **grid 区域中的分隔线**。 object 类型 
- 更多查看：https://echarts.apache.org/zh/option.html#xAxis

 yAxis 选项 ：直角坐标系 grid 中的 y 轴，参数基本和 xAxis 差不多。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175897619600010qtxg.png)


```json
xAxis: {
  show: true,
  name: "类目坐标",
  type: "category", // 类目坐标才有data选项  
  data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"],

  axisLine: { // 坐标轴轴线相关设置。
	show: true,
	lineStyle: {
	  color: "red",
	  width: 3,
	},
  },

  axisLabel: { // 坐标轴刻度标签的相关设置。
	show: true,
	color: "green",
	fontSize: 16,
  },
  
  axisTick: {  // 坐标轴刻度相关设置。
	show: true,
	length: 10,
	lineStyle: {
	  color: "blue",
	  width: 3,
	},
  },
	
  splitLine: { // 坐标轴在 grid 区域中的分隔线。
	show: true,
	lineStyle: {
	  color: "orange",
	  width: 1,
	},
  }, 
},
```

# 四、series系列图配置(组件)

**series：系列，配置系列图表的类型和图形信息数据**。`object[]` 类型，每个object具体配置信息如下 

- name：系列名称，用于**tooltip**的显示，**legend** 的图例筛选等 
- type：指定系列图表的类型，比如：柱状图、折线图、饼图、散点图、地图等 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17589788350005szfni.png)

- data：系列中的数值内容数组。数组中的每一项称为数据项 。 
	- 一维数组: `[ value ， value ] `。（一维数组是二维数组的简写 ） 
	- 二维数组。 
		- `[ [index, value ], [index, value ] ]` ， 注意 index 从 0 开始 
		- `[ [x, y, value ]， [ x, y ， value ] ]`， 注意这里的x 和 y 可以表示x轴和y轴，也可以表示 经度 和 纬度。 
	- 对象类型( 推荐 )。`[ { value: x， name: x， label: { }，itemStyle:{}、 emphasis:{} .... } ]`
- label：图形上的文本标签（**就近原则，data中的比series优先级高**） 
- itemStyle：图形样式。 
- emphasis：高亮的图形样式和标签样式。 
- coordinateSystem：该系列**使用的坐标系**，默认值为二维的直角坐标系（笛卡尔坐标系）

![[00 Echarts5基础学习路线#3.series 系列]]

# 五、series高亮的样式(emphasis)

鼠标悬浮到图形元素上时，高亮的样式。 

- 默认情况高亮的样式是根据普通样式自动生成。但是也可自己定义 
- 自定义主要是通过 **emphasis** 属性来定制。 
- emphsis 的结构和普通样式结构相同，如下图： 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1759041411000i2sdti.png)



ECharts4以前，高亮和普通样式的写法，如下图图

- 这种写法 **仍然被兼容**，但是不再推荐了 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1759041414000yl4hxj.png)


> [!tip]
> 多数情况下，开发者只配置普通状态下的样式， 让高亮的样式是根据普通样式自动生成。


# 六、标题、图例、提示配件(组件)

 title：图表的标题。object 类型。 
 
 - text、top、left.... 
 
 legend：图例，展现了不同系列的标记、颜色和名字。object 类型。 
 
 - show、icon、formatter、textStyle、itemWidth 、itemGap...
 
 tooltip：提示框组件，当鼠标移动到元素上面会有提示。object 类型。
 
 - show、 trigger、axisPointer.....

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1759042321000yjp5hc.png)


# 七、Color和渐变

ECharts中 Color 支持的格式： RGB、RGBA、关键字、十六进制格式 

ECharts中的渐变色 

- 线性渐变，前四个参数分别是（ x, y ）,（ x2, y2 ） 范围从 0 – 1。 
- 径向渐变，前三个参数分别是圆心 x, y 和半径，取值同线性渐变

![gh|300](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17590426690004ovzqb.png)



