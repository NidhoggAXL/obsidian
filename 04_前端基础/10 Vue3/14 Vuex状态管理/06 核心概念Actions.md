# 一、acrions的基本使用
Action类似于mutation，不同在于： 

* Action提交的是mutation，而不是直接变更状态； 
* Action可以包含任意异步操作；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747988746000z2ys31.png)

这里有一个非常重要的参数context： 

* context是一个和store实例均有相同方法和属性的context对象； 
* 所以我们可以从其中获取到commit方法来提交一个mutation，或者通过 context.state 和 context.getters 来获取 state 和 getters；

但是为什么<mark class="hltr-orange">它不是store对象</mark>呢？这个等到我们讲[[07 核心概念Modules|Modules]]时再具体来说；

# 二、actions的分发操作
如何使用action呢？进行action的分发： 

* 分发使用的是 store 上的dispatch函数；
	![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747988849000wpi09m.png)
* 同样的，它也可以携带我们的参数：
	![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747989007000myy5po.png)
* 也可以以对象的形式进行分发：![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17479890220004r2bxy.png)

# 三、actions的辅助函数
action也有对应的辅助函数： 

* 对象类型的写法； ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747989352000yyarnf.png)

* 数组类型的写法；![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17479893580002w37zw.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747989319000wdma1a.png)

# 四、actions的异步操作

Action 通常是异步的，那么如何知道 action 什么时候结束呢？ 

* 我们可以通过让action返回Promise，在Promise的then中来处理完成后的操作；[[07 异步函数|异步函数]]


请求的数据：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747992507000j6z5sj.png)

异步操作

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747992475000ix5u8v.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747992530000yologt.png)


## 4.1 检测异步成功操作

可以更具上面的异步操作继续编写放回值，或者手动放回一个 [[05 Promise的类方法|Promise]]

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747992936000pexwon.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747992942000a54exy.png)

