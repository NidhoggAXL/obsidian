# 一、认识和定义Getters

Getters相当于Store的计算属性（compute）： 

* 它们可以用 defineStore() 中的 **getters 属性**定义； 
* getters中可以**定义接受一个state作为参数的函数**；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748160152000n9hijh.png)

# 二、使用Getters

访问当前store的Getters：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748160187000qs25gb.png)


**Getters中访问自己的其他Getters**：  我们可以通过this来访问到当前store实例的所有其他属性;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748160203000tzgu1m.png)

**访问其他store的Getters**：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748160236000lo2tsf.png)

Getters也可以返回一个函数，这样就可以接受参数：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748160289000h2rwsk.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748160294000rpjc7v.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748160299000wzlkvj.png)

