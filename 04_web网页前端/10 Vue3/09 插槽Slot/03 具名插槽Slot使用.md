# 一、多个插槽的效果
我们先测试一个知识点：如果一个组件中含有**多个插槽**，我们插入多个内容时是什么效果？ 

我们会发现默认情况下<mark class="hltr-orange">每个插槽都会获取到我们插入的内容来显示</mark>；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17467808110009cnjhc.png)


# 二、具名插槽的使用
事实上，我们希望达到的效果是插槽对应的显示，这个时候我们就可以使用 **具名插槽**： 

* 具名插槽顾名思义就是给插槽起一个名字， <mark class="hltr-orange">元素有一个特殊的 attribute：name</mark>； 
* 一个<mark class="hltr-orange">不带 name 的slot，会带有隐含的名字 default</mark>；
	* `<solt></solt> 等价于 <solt name="default"></solt>`
	* 在使用的时候如果不指定插槽名字就会默认使用不带name的插槽

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746780930000grg512.png)


> [!tip] App.vue使用注意事项
> 在使用的具名插槽的时候，需要在使用元素外<mark class="hltr-orange">使用template包裹</mark>，并在template中使用 <mark class="hltr-orange">v-slot: 来确定组件里面要插入地方的名字。</mark>
> 
> <mark class="hltr-orange">还有一些使用方法是，使用 `#` 号来确定要插槽的位置：</mark>
> `<template v-slot:center></template>`等价与`<template #center></template`


# 三、动态插槽名(了解)
什么是动态插槽名呢？

* 目前我们使用的插槽名称都是固定的； 
* 比如 v-slot:left、v-slot:center等等； 
* 我们可以通过 `v-slot:[dynamicSlotName]`方式动态绑定一个名称；
	* dynamic - 动态的

比如：默认是在 center 里面插入按钮的，这个时候通过别的按钮来改变按钮的插入位置。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174678284200074tu2f.png)


