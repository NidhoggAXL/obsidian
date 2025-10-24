# 一、认识侦听器watch

什么是侦听器呢？ 

* 开发中我们在data返回的对象中定义了数据，这个数据通过**插值语法等方式绑定到template中**； 
* 当数据变化时，template会自动进行更新来显示最新的数据； 
* 但是在某些情况下，我们希望在**代码逻辑**中监听某个数据的变化，这个时候就需要用侦听器watch来完成了；

**侦听器的用法如下：** 

* 选项：watch 
* 类型：`{ [key: string]: string | Function | Object | Array}`
* 监听 data 里面的属性时，在 watch 里面的<mark class="hltr-orange">对应函数名必须是和监听 data 的属性相同</mark>
* 监听会默认传入两个参数：参数一（新的属性值）、参数二（旧的参数值）

**当然监听也有语法糖**：[[01 认识事件处理#一、认识事件（Event）|handler]]

```js
watch: {
	//原编写
	info: {
	 handler(newValue, oldValue) {}
	}
	
	//语法糖
	info() { }
}
```


**案例一**：通过按钮来改变data里面的**字符串数据**，但是希望在代码逻辑里面可以监听数据的改变

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745674183000tk8cr5.png)


**案例二**：通过按钮来改变data里面的**对象数据**

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745674607000a84erw.png)

会发现如果改变的是对象就会拿到 [[02 Proxy(代理）类|代理对象]]，如果真的想<mark class="hltr-orange">拿到原对象</mark>，就要使用 **Vue.toRaw()** 方法如下的代码：

```js
console.log(Vue.toRaw(newValue))//{name: 'axl'}
console.log(Vue.toRaw(oldValue))//{name: 'coder', age: 18}

console.log(Vue.toRaw(newValue) === newValue) // true
console.log(Vue.toRaw(oldValue) === oldValue) // true
```

# 二、侦听器watch的配置选项
**我们先来看一个例子：** 

* 当我们点击按钮的时候会修改info.name的值； 
* 这个时候我们使用watch来侦听info，可以侦听到吗？答案是**不可以。**

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745677354000l6xpwz.png)

这是因为默认情况下，<mark class="hltr-orange">watch只是在侦听info的引用变化</mark>，对于<mark class="hltr-orange">内部属性的变化是不会做出响应</mark>的： 

* 这个时候我们可以使用一个选项 **deep** 进行更深层的侦听； 
	* 默认为 false，深度监听为 true
* 注意前面说过**watch里面侦听的属性对应的也可以是一个Object**；

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17456775480007t6azf.png)

> [!tip] 为什么 newValue 和 oldValue 是同一个对象？
> <mark class="hltr-orange">改变的是 info 中的属性 name，并没有改变 info 的地址</mark>，所以说并发生改变我们监听的 info 的地址的，还是对 info 的同一个引用，所以 newValue 和 oldValue 还是同一个对象并且 oldValue 不为 undifined。


**还有另外一个属性，是希望一开始的就会立即执行一次：**

* 这个时候我们使用 **immediate** 选项； 
* 这个时候无论后面数据是否有变化，侦听的函数都会<mark class="hltr-orange">有限执行一次</mark>；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745677910000jycj04.png)




