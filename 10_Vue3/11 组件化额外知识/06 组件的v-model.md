# 一、组件的v-model

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746872071000hooa17.png)

# 二、组件v-model的实现

那么，为了 MyInput组件 可以正常的工作，在这个组件内必须： 

* 将其 value attribute 绑定到一个名叫 modelValue 的 prop 上； 
* 在其 input 事件被触发时，将新的值通过自定义的 update:modelValue 事件抛出； 

MyInput.vue的组件代码如下：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17468814280004llync.png)

# 三、绑定多个属性

前面通过v-model是直接绑定了一个属性，如果我们希望绑定多个属性呢？ 

* 也就是希望在一个组件上使用多个v-model是否可以实现呢？ 
* 我们知道，**默认情况**下的v-model其实是**绑定了 modelValue 属性和 @update:modelValue的事件**； 
* 如果我们希望绑定更多，可以给v-model传入一个参数，那么这个参数的名称就是我们绑定属性的名称； 

**注意**：这里是绑定了两个属性的

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746881488000u0vvxc.png)

v-model:title相当于做了两件事： 

* 绑定了title属性； 
* 监听了 @update:title的事件；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746881511000lndyse.png)

