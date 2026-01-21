# 一、数据的响应

输出结果：body将响应主体设置为以下之一：

 - string ：字符串数据 
 - Buffer ：Buffer数据
 - Stream ：流数据
 - `Object || Array`：对象或者数组
 - null ：不输出任何内容
 - **如果response.status尚未设置，Koa会自动将状态设置为200或204。**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766310726000987wns.png)

请求状态：status

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766310739000vqdjc6.png)

# 二、错误处理

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766312930000sxn9o6.png)
