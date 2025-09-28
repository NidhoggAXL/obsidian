# 一、EChats常见API

全局 echarts 对象，在 script 标签引入 echarts.js 文件后获得，或者在 AMD 环境中通过 require('echarts') 获得。 

- echarts. **init( dom， theme， opts )**：创建echartsInstance实例
- echarts. **registerMap( mapName， opts )**：注册地图 
- echarts. **getMap( mapName )**：获取已注册地图 

通过 echarts.init 创建的实例（echartsInstance） 

- echartsInstance. **setOption(opts)**：设置图表实例的配置项以及数据，万能接口。 
- echartsInstance. getWidth()、 echartsInstance. getHeight()：获取 ECharts 实例容器的宽高度。 
- echartsInstance. **resize(opts)**：改变图表尺寸，在容器大小发生改变时需要手动调用。 
- echartsInstance. **showLoading()**、 echartsInstance. **hideLoading()**：显示和隐藏加载动画效果。 
- echartsInstance. dispatchAction( )：触发图表行为，例如：图例开关、显示提示框showTip等 
- echartsInstance. dispose：销毁实例，销毁后实例无法再被使用 
- echartsInstance. **on()**：通过 on 方法添加事件处理函数，该文档描述了所有 ECharts 的事件列表。

# 二、响应式ECharts图表

响应式图片的实现步骤： 

1. 图表**只设置高度**，宽度设置为100% 或 不设置。 
2. 监听窗口的resize事件，即监听窗口尺寸的变化（需节流）。 
3. 当窗口大小改变时，然后调用 **echartsInstance.resize** 改变图表的大小。。

另外需要注意的是： 在容器节点被销毁时，可以调用 **echartsInstance.dispose** 以销毁echarts的实例释放资源，避免内存泄漏。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17590629120005hbnrq.png)


