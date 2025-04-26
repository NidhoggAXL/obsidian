# 一、v-for中的key是什么作用？
在使用v-for进行列表渲染时，我们通常会给元素或者组件绑定一个key属性。

这个key属性有什么作用呢？我们先来看一下 **官方的解释**： 

* key属性主要用在Vue的 **虚拟DOM算法**，在**新旧nodes**对比时辨识 **VNodes**； 
* 如果**不使用key**，Vue会使用一种最大限度减少动态元素并且尽可能的尝试就地**修改/复用相同类型**元素的算法； 
* 而**使用key时**，它会基于key的变化**重新排列元素顺序**，并且会移除/销毁key不存在的元素；

官方的解释对于初学者来说并不好理解，比如下面的问题： 

* 什么是新旧nodes，什么是VNode？ 
* 没有key的时候，如何尝试修改和复用的？
* 有key的时候，如何基于key重新排列的？


# 二、认识VNode

我们先来解释一下VNode的概念： 

* 因为目前我们还没有比较完整的学习组件的概念，所以目前我们先理解HTML元素创建出来的VNode； 
* VNode的全称是Virtual Node，也就是**虚拟节点**； 
* 事实上，无论是 **组件还是元素**，它们最终 **在Vue中表示出来的都是一个个VNode**；
* <mark class="hltr-orange">VNode的本质是一个JavaScript的对象；</mark>

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745656355000yam4d8.png)




