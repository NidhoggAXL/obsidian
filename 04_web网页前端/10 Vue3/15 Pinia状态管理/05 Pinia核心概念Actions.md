# 一、认识和定义Actions
Actions 相当于组件中的 methods。 

* 可以使用 defineStore() 中的 actions 属性定义，并且它们非常适合定义业务逻辑；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748161863000szfegd.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748161867000dqcgt9.png)

和getters一样，在action中可以通过<mark class="hltr-orange">this访问整个store实例</mark>的所有操作；

# 二、Actions执行异步操作

并且Actions中是支持异步操作的，并且我们可以编写异步函数，在函数中使用await；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748161924000welyyv.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748161929000754eg4.png)

