# 一、全局app配置文件
全局配置比较多, 我们这里将几个比较重要的. 完整的查看官方文档. 

* https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753533315000duswme.png)

**pages: 页面路径列表** 

* 用于指定小程序由哪些页面组成，每一项都对应一个页面的 路径（含文件名） 信息。 
* 小程序中所有的页面都是必须在pages中进行注册的。 

**window: 全局的默认窗口展示** 

* 用户指定窗口如何展示, 其中还包含了很多其他的属性

**tabBar: 顶部tab栏的展示** 

* 具体属性稍后我们进行演示

# 二、配置案例实现

案例要求：显示底部的 tabBar，并可以点击进行 page 的跳转：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17535335310001dy5y5.png)


