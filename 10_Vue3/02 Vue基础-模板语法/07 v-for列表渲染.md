# 一、列表渲染
在真实开发中，我们往往会从服务器拿到**一组数据**，并且需要对其进行渲染。 

* 这个时候我们可以使用**v-for**来完成； 
* v-for类似于JavaScript的for循环，可以用于遍历一组数据；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745651549000dfwk4v.png)

# 二、v-for基本使用

v-for的基本格式是 **"item in 数组"**： 

* 数组通常是来自 **data或者prop**，也可以是其他方式； 
* item是我们给每项元素起的一个**别名**，这个别名可以自定来定义；
* <mark class="hltr-yellow">也可以i使用 "item of 数组"，结果是一样的</mark>

我们知道，在遍历一个数组的时候会经常需要拿到**数组的索引：**

* 如果我们需要索引，可以使用格式： **"(item, index) in 数组"**； 
* 注意上面的顺序：数组元素项item是在前面的，索引项index是在后面的；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745652197000kgk7bx.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17456522070009xrqjj.png)







