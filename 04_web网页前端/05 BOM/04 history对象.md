> [!tip] 前端路由核心:修改URL，但是页面不刷新
> 1. 修改hash值
> 2. 修改history
> **有什么用呢？**
> 当我们再不同页面中有相同的部分的时候，只需要修改hash值或者history值，来渲染不同页面中不同的部分，就不需要再向服务器发送请求啦。

# 一、history对象常见的属性和方法
history对象允许我们访问浏览器曾经的会话历史记录。

有两个属性:

* length:会话中的记录条数
* state:当前保留的状态值;

有五个方法:

* back():返回上一页，等价于history.go(-1);
* forward():前进下一页，等价于history.go(1);
* go():加载历史中的某一页;
* pushState():打开一个指定的地址;
* replaceState():打开一个新的地址，并且使用replace;


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17291749250006xzqhp.png)

> history和hash目前是vue、react等框架实现路由的底层原理


