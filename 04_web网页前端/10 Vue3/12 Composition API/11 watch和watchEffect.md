# 一、监听数据的变化
在前面的Options API中，我们可以通过[[04 监听器watch选项使用|watch]]选项来侦听data或者props的数据变化，当数据变化时执行某一些操作。 

在Composition API中，我们可以使用watchEffect和watch来完成响应式数据的侦听； 

* watchEffect：用于自动收集响应式数据的依赖； 
* watch：需要手动指定侦听的数据源；
# 二、watch的使用
watch的API完全等同于组件watch选项的Property： 

* watch需要<mark class="hltr-orange">侦听特定的数据源</mark>，并且执行其回调函数； 
* 默认情况下它是惰性的，只有当被侦听的源发生变化时才会执行回调；

```js
import { ref, watch } from 'vue'
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747575335000w404h5.png)

# 三、侦听多个数据源
侦听器还可以使用数组同时侦听多个源：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17475753920002oes6n.png)

# 四、watch的选项
如果我们希望侦听一个深层的侦听，那么依然需要设置 <mark class="hltr-orange">deep 为true： </mark>

* 也可以传入 immediate 立即执行；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747575464000rrvyai.png)

# 五、watchEffect
当侦听到某些响应式数据变化时，我们希望执行某些操作，这个时候可以使用 <mark class="hltr-orange">watchEffect</mark>。

**我们来看一个案例：** 

* 首先，watchEffect传入的函数<mark class="hltr-orange">会被立即执行一次</mark>，并且在执行的过程中<mark class="hltr-orange">会收集依赖</mark>； 
* 其次，<mark class="hltr-orange">只有</mark>收集的依赖发生变化时，watchEffect传入的函数才会再次执行；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747575541000a2tdui.png)

> 例如上面的例子：这里的依赖就是 name 和 age

# 六、watchEffect的停止侦听
如果在发生某些情况下，我们希望停止侦听，这个时候我们可以获取watchEffect的<mark class="hltr-orange">返回值函数，调用该函数</mark>即可。 

比如在上面的案例中，我们age达到20的时候就停止侦听：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747575675000aq3qkl.png)
