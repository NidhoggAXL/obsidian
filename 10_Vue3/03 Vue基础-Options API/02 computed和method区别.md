# 一、computed VS mesthods

会发现计算属性和methods的实现看起来是差别是不大的，而且我们多次提到计算属性<mark class="hltr-orange">有缓存</mark>的。

* 接下来我们来看一下同一个计算多次使用，计算属性和methods的差异：

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17456613600007yzdl8.png)

methods 中的 getName 调用了3次，而 pullName 却只是调用了一次。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745661368000e9kl3j.png)


# 二、computed属性的缓存

这是什么原因呢？ 

* 这是因为计算属性会基于它们的<mark class="hltr-orange">依赖关系进行缓存</mark>； 
* 在**数据不发生变化**时，计算属性是不需要重新计算的； 
* 但是如果依赖的数据发生变化，在使用时，**计算属性依然会重新进行计算**；

案例：如上面代码，当按钮点击的时候，lastName发生改变

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745661583000uhbv4v.png)

当点击按钮该改变 lastName 时：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174566162700073al1h.png)




