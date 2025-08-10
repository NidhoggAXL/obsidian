# 一、Reactive API
如果想为在setup中定义的数据提供响应式的特性，那么我们可以<mark class="hltr-orange">使用reactive的函数</mark>：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747550407000z719sd.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747550417000a1y4in.png)

# 二、Ref API

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747550511000u59t0d.png)

# 三、Ref自动解包
<mark class="hltr-orange">模板中的解包是浅层的解包</mark>，如果我们的代码是下面的方式：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17475506570005241s8.png)


如果我们<mark class="hltr-orange">将ref放到一个reactive的属性</mark>当中，那么在模板中使用时，它<mark class="hltr-orange">会自动解包</mark>：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747550716000hssrab.png)


# 四、开发中reactive和ref选择
reactive的应用场景

* 条件一:reactive应用于本地的数据
* 条件二:多个数据之间是有关系|联系(聚合的数据，组织在一起会有特定的作用)

例如用户名和密码就应该使用reactive来使用，这些数据都是具有一定的联系的。

ref的应用场景:

* 其他的场景基本都用ref(computed)
* 定义本地的一些简单数据
* 定义从网络中获取的数据也是使用ref
