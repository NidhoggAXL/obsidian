我们会发现，所有的节点、元素都继承自EventTarget

* 事实上Window也继承自EventTarget;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1734165815000mj89bd.png)

那么这个EventTarget是什么呢?

* EventTarget是一个DOM接口主要用于添加、删除、派发Event事件;

EventTarget常见的方法:

* **addEventListener**:注册某个事件类型以及事件处理函数，
* **removeEventListener**:移除某个事件类型以及事件处理函数:
* **dispatchEvent**:派发某个事件类型到EventTarget上;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17341658920005i9bex.png)

