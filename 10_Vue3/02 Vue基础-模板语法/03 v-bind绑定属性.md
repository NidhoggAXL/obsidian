# 一、v-bind绑定属性

前端讲的一系列指令，主要是将值插入到**模板内容**中。

但是，除了内容需要动态来决定外，某些属性我们也希望动态来绑定

- 比如动态绑定 a 元素的 href 属性
- 比如动态绑定 img 元素的 src 属性:


绑定属性我们使用v-bind:

- 缩写 `:`
- 预期: `any (with argument)|Object (without argument)` 
- 参数: `attrOrProp (optional)`
- 修饰符
	- `.camel`-将 kebab-case attribute 名转换为 camelCase.
- 用法:**动态地绑定一个或多个 attribute，或一个组件 prop 到表达式**。


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745501325000quyqrl.png)

> [!note]
> v-bind有一个对应的语法糖，也就是简写方式。 
> 在开发中，我们通常会使用语法糖的形式，因为这样更加简洁。
# 二、绑定基本属性

v-bind用于**绑定一个或多个属性值**，或者向另一个组件[[03 父组件传递子组件|传递props值]]

在开发中，有哪些属性需要动态进行绑定呢？ 

* 还是有很多的，比如图片的链接src、网站的链接href、动态绑定一些类、样式等等

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17455016690009nrxqn.png)

当使用了 v-bind 绑定属性后，引号里面的也可以编写为一个表达式

```html
<div :class=" 2 > 3 ? true : flase"></div>
```










