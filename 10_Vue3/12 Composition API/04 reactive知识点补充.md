# 一、认识readonly

通过reactive或者ref可以获取到一个响应式的对象，但是某些情况下，传入给其他地方(组件)的这个响应式对象希望在**另外一个地方(组件)被使用，但是不能被修改**，这个时候如何防止这种情况的出现呢?

- Vue3提供了 **readonly** 的方法。
- readonly 会**返回原始对象的只读代理**(也就是它依然是一个 [[02 Proxy代理类|Proxy]]，这是一个 proxy 的set方法被劫持，并且不能对其进行修改)

> [!abstract]
> 
> 这种另一个组件不可以修改传入的数据方式，就是一种数据的单向流。

在开发中常见的readonly方法会传入三个类型的参数:

- 类型一:普通对象
- 类型二:reactive返回的对象
- 类型三:ref的对象

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747554767000baj2is.png)

# 二、readonly的使用

在readonly的使用过程中，有如下规则:

- **readonly返回的对象都是不允许修改的**
- 但是经过readonly处理的**原来对象**是允许被修改的;
	- 比如 `const info = readonly(obj)`，info对象是不允许被修改的
	- 当obj被修改时，readonly返回的info对象也会被修改
	- 但是我们不能去修改readonly返回的对象info

> [!abstract] 
> 
> 其实本质上就是readonly返回的对象的setter方法被劫持了而已

# 三、readonly的应用

那么这个readonly有什么用呢？ 

在传递给其他组件数据时，往往希望其他组件使用传递的内容，但是不允许它们修改时，就可以使用readonly了；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747554831000qc6l6e.png)

编写下面的代码，那么 home 组件里面的事件就不会修改传入的 info 数据：

![gh|400](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747554837000wrdxvq.png)

# 四、Reactive判断的API

isProxy：检查对象是否是由reactive 或 readonly创建的 proxy。

isReactive：

 - 检查对象是否是由reactive创建的响应式代理:
 - 如果该代理是readonly 建的，但包裹了由reactive创建的另一个代理，它也会返回true;

isReadonly：检查对象是否是由 readonly 创建的只读代理。

toRaw：返回reactive或readonly代理的原始对象(**不建议保留对原始对象的持久引用。请谨慎使用**)。

shallowReactive：创建一个响应式代理，它跟踪其自身property的响应性，但不执行嵌套对象的深层响应式转换(**深层还是原生对象**)。

shallowReadonly：创建一个proxy，使其自身的property为只读，但不执行嵌套对象的深度只读转换(**深层还是可读、可写的**)




