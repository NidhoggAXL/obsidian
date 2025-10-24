
# 一、计算属性的setter和getter
计算属性在大多数情况下，只需要一个**getter方法**即可，所以我们会将计算属性直接**写成一个函数**。 

```js
// 完整编写发法
pullName: {
 get() { console.log("hahah") }
}

// 语法糖写法
pullName() { console.log("hahahah") }
```

但是，如果我们确实想**设置计算属性的值**呢？ (<mark class="hltr-orange">了解</mark>)

* 这个时候我们也可以给计算属性设置一个setter的方法；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745672564000p3y2qu.png)


# 二、源码如何对setter和getter处理呢？（了解）

你可能觉得很奇怪，Vue内部是如何对我们传入的是一个getter，还是说是一个包含setter和getter的对象进行处理的呢？ 

* 事实上非常的简单，Vue源码内部只是做了一个逻辑判断而已；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174567272200063zcvp.png)





