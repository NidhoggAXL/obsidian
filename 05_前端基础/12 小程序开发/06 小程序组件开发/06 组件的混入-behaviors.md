behaviors 是用于组件间代码共享的特性，类似于一些编程语言中的 [[07 组件的混入Mixin(了解)|mixins]]。 

- 每个 behavior 可以包含**一组属性、数据、生命周期函数和方法**； 
- 组件引用它时，它的**属性、数据和方法**会被合并到组件中，生命周期函数也会在对应时机被调用； 
- 每个组件可以**引用多个** behavior ，behavior 也可以引用其它 behavior ；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17537706600003w4gpn.png)


