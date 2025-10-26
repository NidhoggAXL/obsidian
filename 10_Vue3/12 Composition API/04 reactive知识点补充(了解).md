# 一、认识readonly

通过reactive或者ref可以获取到一个响应式的对象，但是某些情况下，传入给其他地方(组件)的这个响应式对象希望在**另外一个地方(组件)被使用，但是不能被修改**，这个时候如何防止这种情况的出现呢?

- Vue3提供了 **readonly** 的方法。
- readonly 会**返回原始对象的只读代理**(也就是它依然是一个 Proxy，这是一个 proxy 的set方法被劫持，并且不能对其进行修改)

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
	- <mark class="hltr-cyan">当obj被修改时，readonly返回的info对象也会被修改</mark>
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

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174755708600053ps36.png)



