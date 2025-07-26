# 一、异步组件和Suspense

什么是异步组件：[[05 异步组件的使用|异步组件]]

> [!tip] 注意：目前（2025-07-27）Suspense显示的是一个实验性的特性，API随时可能会修改。

Suspense是一个内置的全局组件，该组件有两个插槽： 

* default：如果default可以显示，那么显示default的内容； 
* fallback：如果default无法显示，那么会显示fallback插槽的内容；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17534064810006z2ils.png)

