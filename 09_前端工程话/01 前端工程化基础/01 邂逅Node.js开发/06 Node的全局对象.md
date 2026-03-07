# 一、常见的全局对象

Node中给我们提供了一些全局对象，方便我们进行一些操作:

* 这些全局对象，我们并不需要从一开始全部一个个学习
* 某些全局对象并不常用
* 某些全局对象我们会在后续学习中讲到
	* 比如module、exports、require()会在模块化中讲到,
	* 比如 [[04 Buffer|Buffer]] 后续会专门讲到:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743748463000c0a9dr.png)

# 二、特殊的全局对象

为什么我称之为特殊的全局对象呢?

 * 这些全局对象实际上是**模块中的变量**，只是每个模块都有，**看来像是全局变量**;

 在命令行交互中是不可以使用的;

* 包括: dirname、filename、**exports、module、require()**

**`__dirname`**:获取当前文件所在的路径

* **注意**:不包括后面的文件名

**`__filename`**:获取当前文件所在的路径和文件名称:

* **注意**:包括后面的文件名称

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743748832000y4x79k.png)

# 三、常见的全局对象

**process对象**:process提供了Node进程中相关的信息:

* 比如Node的运行环境、参数信息等;
* 后面在项目中，我也会讲解，如何将一些环境变量读取到 process 的env中

console对象:提供了简单的调试控制台，在前面讲解输入内容时已经学习过了，更加详细的查看官网文档:https://nodeis.orq/api/console.html

定时器函数:在Node中使用定时器有好几种方式:

* **`setTimeout(callback, delay[,...args])`**:callback在delay毫秒后执行一次;
* **`setlnterval(callback,delay[,..args])`**:callback每delay毫秒重复执行一次;
* **`setlmmediate(callback[,..args])`**:callback的l/O事件后的回调的“立即”执行;
	* 这里先不展开讨论它和setTimeout(callback,0)之间的区别;
	* 因为它涉及到事件循环的阶段问题，我会在后续详细讲解[[02 浏览器进程、线程|事件循环]]相关的知识;
* **`process.nextTick(callback[, .args])`**:添加到下-次tick队列中;具体的讲解，也放到事件循环中说明;

# 四、global对象

global是一个全局对象，事实上前端我们提到的process、console、setTimeout等都有被放到global中:

* 我们之前讲过:在新的标准中还有一个globalThis，也是指向全局对象的;
* 类似于浏览器中的window:

![[Node和Window中全局对象的区别]]


# 五、blobal和window的区别

在浏览器中，全局变量都是在window上的，比如有document、setinterval、setTimeout、alert、console等等

在Node中，我们也有一个global属性，并且看起来它里面有很多其他对象。


但是在浏览器中执行的JavaScript代码，如果我们在顶级范围内通过var定义的一个属性，默认会被添加到window对象上:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743751529000t4wsod.png)

但是在node中，我们通过var定义一个变量，它只是在当前模块中有一个变量，不会放到全局中:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743751544000bgb4bk.png)

