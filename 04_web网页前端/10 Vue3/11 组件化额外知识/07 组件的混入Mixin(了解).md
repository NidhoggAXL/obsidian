# 一、认识Mixin
目前我们是使用组件化的方式在开发整个Vue的应用程序，但是**组件和组件之间有时候会存在相同的代码逻辑**，我们希望对相同 **的代码逻辑进行抽取**。

在Vue2和Vue3中都支持的一种方式就是**使用Mixin来完成**： 

* Mixin提供了一种非常灵活的方式，来<mark class="hltr-orange">分发Vue组件中的可复用功能</mark>； 
* 一个Mixin<mark class="hltr-orange">对象</mark>可以包含<mark class="hltr-orange">任何组件选项</mark>； 
* 当组件使用Mixin对象时，所有<mark class="hltr-yellow">Mixin对象的选项将被 混合 进入该组件本身的选项中</mark>

# 二、Mixin的基本使用

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746882611000d9ye19.png)

# 三、Mixin的合并规则

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746882727000iw4s77.png)

# 四、全局混入Mixin
如果组件中的某些选项，是所有的组件都需要拥有的，那么这个时候我们可以使用**全局的mixin：** 

* 全局的Mixin可以使用 <mark class="hltr-orange">应用app的方法</mark> mixin 来完成注册； 
* 一旦注册，那么<mark class="hltr-orange">全局混入的选项将会影响每一个组件</mark>；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17468828220001i7pat.png)







