# 一、认识z-index
**z-index属性用来设置定位元素的层叠顺序(仅对定位元素有效)**

* 取值可以是正整数、负整数、0


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723536555000zd2p79.png)

**比较原则：**

* 如果是兄弟关系
	* z-index越大，层叠在越上面
	* z-index相等，写在后面的那个元素层叠在上面
* 如果不是兄弟关系
	* 各自从元素自己以及祖先元素中，找出最邻近的2个定位元素进行比较
	* 而且这2个定位元素必须有设置z-index的具体数值




