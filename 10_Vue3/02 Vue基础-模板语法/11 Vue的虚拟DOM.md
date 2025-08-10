
# 一、认识VNode

我们先来解释一下VNode的概念： 

* 因为目前我们还没有比较完整的学习组件的概念，所以目前我们先理解HTML元素创建出来的VNode； 
* VNode的全称是Virtual Node，也就是**虚拟节点**； 
* 事实上，无论是 **组件还是元素**，它们最终 **在Vue中表示出来的都是一个个VNode**；
* <mark class="hltr-orange">VNode的本质是一个JavaScript的对象；</mark>

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745656355000yam4d8.png)

# 二、虚拟DOM是什么

如果我们不只是一个简单的div，而是有一大堆的元素，那么它们应该会形成一个VNode Tree：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745656381000mjbn6v.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745656393000yjwfjo.png)


# 三、虚拟DOM的作用

**可以进行跨平台使用，因为虚拟DOM本质上是一个个<mark class="hltr-blue"> JavaScript对象</mark>，如果是一个对象那么就可以通过不同的方法使用到不同的设备上面。**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17456561680004fgjjk.png)




