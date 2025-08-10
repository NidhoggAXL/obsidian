# 一、v-**for支持的类型**
v-for也支持遍历对象，并且支持有一二三个参数： 

* 一个参数： "value in object"; 
* 二个参数： "(value, key) in object"; 
* 三个参数： "(value, key, index) in object"; 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745653174000zg7xqg.png)


v-for同时也支持数字的遍历： 

* 每一个item都是一个数字；

```html
<li v-for="item in 10">{{item}}</li>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745653273000ypbctt.png)


v-for也可以遍历其他(Iterable)[[01 迭代器和可迭代对象#二、可迭代对象|可迭代对象]]




