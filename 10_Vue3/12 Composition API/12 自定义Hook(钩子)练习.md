# 一、useCounter

就是对计数器进行一个逻辑的抽取：

例如把计数器的逻辑抽取到 useCounter.js 文件里面，再在 App.vue 里面使用：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747634937000ca9z5k.png)

在 App.vue 里面进行return的时候也可以使用[[06 展开运算符|展开运算符]]：

```js
return {
	...useCounter()
}
```

# 二、useTitle

编写一个修改title的Hook：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747636199000bpld6d.png)

# 三、useScrollPositon

完成一个监听界面滚动位置的Hook：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747636561000h2ubwg.png)








