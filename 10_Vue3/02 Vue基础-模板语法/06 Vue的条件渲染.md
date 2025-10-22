# 一、条件渲染·

在某些情况下，我们需要根据当前的条件决定**某些元素或组件是否渲染**，这个时候我们就需要进行条件判断了。

Vue提供了下面的指令来进行条件判断： 

* v-if 
* v-else 
* v-else-if 
* v-show

**案例一**：v-if 和 v-else 的联合使用，names 里面有数据则列表显示，如果没有则显示 h2 标签的内容。

![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745648557000ftqa8y.png)


**案例二**：v-else-if 的使用，成绩好坏的判断

![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17456494210000b59a5.png)

**v-if的渲染原理：** 

* v-if是惰性的； 
* 当条件为false时，其判断的内容**完全不会被渲染或者会被销毁掉**； 
* 当条件为true时，才会**真正渲染**条件块中的内容；

例如如下：h2 为false后就不会在页面的和html中

```html
<h2 v-if="false">{{ count }}</h2>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17469541490007fs4sk.png)
# 二、template元素

因为v-if是一个指令，所以必须将其添加到一个元素上：

* 但是如果我们希望切换的是多个元素呢？ 
* 此时我们渲染div，但是我们<mark class="hltr-orange">并不希望div这种元素被渲染</mark>； 
* 这个时候，我们可以选择使用 template； 

template元素可以当做不可见的**包裹元素**，并且在 **v-if上使用**，但是最终template**不会被渲染出来**： 

* 有点类似于小程序中的block

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745650447000xndxfa.png)


# 三、v-show

v-show和v-if的用法看起来是一致的，也是根据一个条件决定是否显示元素或者组件：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17456509740008wz5l3.png)


## 3.1 v-show和v-if的区别

首先，在用法上的区别： 

* v-show是**不支持**template； 
* v-show不可以和v-else一起使用； 


其次，本质的区别：
* v-show元素无论是否需要显示到浏览器上，它的**DOM实际都是有存在的**，只是通过CSS的display属性来进行切换； 
* v-if当条件为false时，其对应的原生压根不会被渲染到DOM中； 

```html
<h2 v-if="false">{{ count }}</h2>
<h2 v-show="false">{{ count }}</h2>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174695431900068ebpl.png)


**开发中如何进行选择呢？**

* 如果我们的原生需要在显示和隐藏之间**频繁的切换**，那么使用v-show；
* 如果不会频繁的发生切换，那么使用v-if；












