# 一、初体验SVG

如何绘制一个SVG矢量图？ 绘制SVG矢量图常用有4种方式： 

- 方式一：在一个单独的svg文件中绘制，svg文件可直接在浏览器预览或嵌入到HTML中使用（**推荐**）
- 方式二：直接在HTML文件中使用svg元素来绘制（**推荐**） 
- 方式三：直接使用JavaScript代码来生成svg矢量图。 
- 方式四：使用AI（Adobe IIIustractor）矢量绘图工具来绘制矢量图，并导出为svg文件（**推荐**）

SVG 初体验：

- 第一步：新建一个 svg 文件，在文件第一行编写**XML文件声明** 
- 第二步：编写 一个元素，并给该元素添加如下属性：
	- ~~version~~： 指定使用svg的版本，值为 1.0 和 1.1，并没有 2.0。 
	- ~~baseProfile~~：SVG 2 之前，version 和 baseProfile 属性用来验证和**识别 SVG 版本**。而SVG2后不推荐使用这两个属性了。
	- width / height ：指定svg画布（视口）的宽和高，**默认值分别为300和150**，默认使用px单位。 
	- xmlns：给svg元素帮定一个命名空间（http://www.w3.org/2000/svg）意味着这个 `<svg> ` 标签和它的子元素都属于该命名空间下。
		- **svg 2.0 后浏览器会自动添加**
- 第三步：在 `<svg>` 元素中添加 图形（比如：`<rect>` ） 元素 
- 第四步：在浏览器直接预览 或 嵌入到 HTML中预览（嵌入HTML有6种方案）



# 二、XML和DTD声明

由于 SVG 是一个 XML 文件格式。在编写XML文档时，通常是推荐编写XML声明。因为**在 XML 1.0 中，XML 声明是可选的，推荐写但不是强制性**。

然而，在 XML 1.1 中，声明是强制性的，如果没有声明，则自动暗示该文档是 XML 1.0 文档。所以这里**建议在编写SVG文件时也编写一个 XML 声明**。

SVG的XML声明格式：`<?xml version='1.0' encoding='UTF-8' standalone='no' ?>`

- version 指定版本（**必填**） 
- encoding 指定XML文档的编码（可选，默认是UTF-8） 
- standalone：指定当前 XML 文档**是否依赖于外部标记声明**（可选，使用该属性时，**需和DTD声明一起用才有意义**）。
	- 默认为no：代表**依赖外部标记声明** 
	- yes：代表依赖内部默认的标记声明

**VG的文档类型声明（DTD）**，让解析器验证XML文件是否符合该规范，与HTML5文件的DTD声明类似。 

- XML中内部 DTD 声明（可选） ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758509422000lcm485.png)

- XML中外部 DTD 声明（可选）![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758509426000d16qp8.png)
声明文件代码：

```svg
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
```

# 三、SVG文档结构

SVG1.1文档结构:https://www.w3.org/TR/SVG11/struct.html 

- 第一行：包含一个 XML 声明。由于 SVG 文件是一个 XML 格式的，它应包含一个 XML 声明。 
- 第二行：定义文档类型声明 (DTD)，这里依赖外部的 SVG1.1 文档类型，让解析器验证XML文件是否符合该规范。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758511457000ue335f.png)

SVG2.0文档结构:https://www.w3.org/TR/SVG2/struct.html#Namespace 

- SVG2 version和baseProfile属性已删除，也不推荐写文档类型声明（DTD）。其中 `<desc>` 元素是用来描述文件的。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175851829100070ggmq.png)

# 四、JS 创建 SVG

使用JS脚本来创建SVG时，创建的元素都是需要添加命名空间的。 

- 比如：创建 `<svg>` 或者 `<rect>` 元素都需要添加命名空间（http://www.w3.org/2000/svg） 
- 对于元素上的属性如果不带前缀的，命名空间赋值为null。 

因为在XML1.1命名空间规范中建议，**不带前缀的属性**（带前缀xlink:href）命名空间的名称是没有值的，这时命名空间的值必须 **使用null值**。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758518952000ww5fsj.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758519023000sybdbj.png)

创建 SVG 常用的 DOM2 API： 

- createElementNS（ns，elname）：创建SVG元素 
- setAttributeNS（ns，attrname，value）：给SVG元素添加属性 
- getAttributeNS（ns，attrname）：获取SVG元素上的属性 
- hasAttributeNS（ns, attrname）： 判断SVG元素上是否存在某个属性 
- removeAttributeNS（ns，attname）：删除SVG元素上的某个属性 
- 更多的API：https://developer.mozilla.org/zh-CN/docs/Web/SVG/Namespaces_Crash_Course


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175851883900045mz76.png)

# 五、HTML引入SVG

**方式一：img元素** 

- 作为一张图片使用，不支持交互，只兼容ie9以上 

**方式二：CSS背景** 

- 作为一张背景图片使用，不支持交互

**方式三：直接在HTML文件引用源文件** 

- 作为HTML 的DOM元素，支持交互，只兼容ie9以上

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758519972000dpf70c.png)


方式四：object元素（了解）。 

- 支持交互式 svg，能拿到object的引用，为 SVG 设置动画、更改其样式表等

方式五：iframe元素（了解） 。 

- 支持交互式 svg，能拿到iframe的引用，为 SVG 设置动画、更改其样式表等

方式六：embed元素（了解） 。 

- 支持交互式 svg，能拿到embed的引用，为 SVG 设置动画、更改其样式表等，对旧版浏览器有更好的支持。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758520046000927orl.png)





