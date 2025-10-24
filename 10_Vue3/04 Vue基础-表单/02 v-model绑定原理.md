# 一、v-model的原理

官方有说到，v-model的原理其实是背后有两个操作： 

* v-bind绑定value属性的值； 
* v-on绑定input事件监听到函数中，函数会获取最新的值赋值到绑定的属性中；

```html
<input v-model="searchText" />
```

等价与

```html
<input :value="searchText" @input="searchText = $sevent.target.value" />
```

# 二、事实上v-model更加复杂

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745932303000x9nmz7.png)

