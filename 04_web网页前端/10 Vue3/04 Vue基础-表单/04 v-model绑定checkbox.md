看一下v-model绑定 **checkbox**：单个勾选框和多个勾选框 

<mark class="hltr-orange">单个勾选框： </mark>

* v-model即为**布尔值。** 
* 此时input的value属性并不影响v-model的值。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745933579000r1cfe1.png)

<mark class="hltr-orange">多个复选框： </mark>

* 当是**多个复选框**时，因为可以选中多个，所以对应的**data中属性是一个数组**。 
* 当选中某一个时，就会**将input的value添加到数组中。**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745933590000rbxeef.png)




