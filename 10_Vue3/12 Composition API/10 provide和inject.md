# 一、Provide函数

事实上我们之前还学习过[provide和inject](10_Vue3/10%20非父子组件间通信/01%20依赖注入Provide和lnject.md)，Composition APl也可以替代之前的 Provide 和 Inject 的选项。

通过 provide来提供数据: provide 方法来定义每个 Property;

provide可以传入两个参数:

* name:提供的属性名称，
* value:提供的属性值;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747574057000rmsm5v.png)

# 二、inject函数

在 **后代组件** 中可以通过 inject 来注入需要的属性和对应的值

inject可以传入两个参数： 

* 要 inject 的 property 的 name； 
* 默认值；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747574101000gna3u7.png)

# 三、数据响应式

为了增加 provide 值和 inject 值之间的响应性，我们可以在 provide 值时使用 [ref 和 reactive](10_Vue3/12%20Composition%20API/03%20setup中数据的响应式.md)。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747574137000jigzti.png)


