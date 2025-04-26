# 一、认识侦听器watch

什么是侦听器呢？ 

* 开发中我们在data返回的对象中定义了数据，这个数据通过**插值语法等方式绑定到template中**； 
* 当数据变化时，template会自动进行更新来显示最新的数据； 
* 但是在某些情况下，我们希望在**代码逻辑**中监听某个数据的变化，这个时候就需要用侦听器watch来完成了；

侦听器的用法如下： 

* 选项：watch 
* 类型：`{ [key: string]: string | Function | Object | Array}`
* 监听 data 里面的属性时，在 watch 里面的对应函数必须是和监听 data 的属性相同
* 监听会默认传入两个参数：参数一（新的属性值）、参数二（旧的参数值）


**案例一**：通过按钮来改变data里面的**字符串数据**，但是希望在代码逻辑里面可以监听数据的改变

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745674183000tk8cr5.png)


**案例二**：通过按钮来改变data里面的对象数据

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745674607000a84erw.png)

会发现如果改变的是对象就会拿到 [[02 Proxy(代理）类|代理对象]]，如果真的想<mark class="hltr-orange">拿到原对象</mark>，就要使用 **Vue.toRaw()** 方法如下的代码：

```js
console.log(Vue.toRaw(newValue))//{name: 'axl'}
console.log(Vue.toRaw(oldValue))//{name: 'coder', age: 18}

console.log(Vue.toRaw(newValue) === newValue) // true
console.log(Vue.toRaw(oldValue) === oldValue) // true
```

# 二、
