# 一、认识高阶组件

高阶函数的维基百科定义：至少满足以下条件之一： 

- 接受一个或多个函数作为输入； 
- 输出一个函数；

JavaScript中比较常见的filter、map、reduce都是高阶函数。

那么说明是高阶组件是什么呢？ 

- 高阶组件的英文是 Higher-Order Components，简称为 HOC； 
- 官方的定义：高阶组件是参数为组件，返回值为新组件的<mark class="hltr-orange">函数</mark>；

**可以进行如下的解析**： 

- 首先， 高阶组件 **本身不是一个组件，而是一个函数**； 
- 其次，这个函数的**参数是一个组件**，**返回值也是一个组件**；
- 本质目的是**对传入的组件做一个拦截**，在这个拦截里面可以进行操作。

# 二、高阶组件的定义

高阶组件的调用过程类似于这样：

```jsx
const EnhanceComponent = higherOrderComponent(WarppedComponent)
```

高阶组件的编写·过程类似如下：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755260104000vkbm06.png)

**组件的名称问题**： 

- 在ES6中，类表达式中类名是可以省略的； 
- 组件的名称都可以通过displayName来修改；

> [!tip] 高阶组件并不是React API的一部分，它是基于React的 组合特性而形成的设计模式； 
> 
> 高阶组件在一些React第三方库中非常常见： 
> 
> - 比如redux中的 **connect**；
> - 比如react-router中的 **withRouter**；

# 三、高阶组件的应用

## 3.1 props的增强

![[React高阶组件增强Propos|100%]]

> [!info] 封装的方式有两种：
> - 使用类组件来重新渲染传入的组件
> 	- 需要增强的 数据 在创建高阶组件的时候就是确定好了，
> - 使用函数组件来重新渲染传入的组件
> 	- 需要增强的 数据 每一次都需要进行确定，
> - 使用总结：
> 	- 需要增强的组件 类组件和函数组件 对比，类组件多了可以在自身添加 this.state 数据，再次添加本地数据
> 	- 两种封装的方法，各有好处，类封装可以不用每次确定需要增强的数据，函数封装可以改变增强的数据

> [!tip] 总结 
> - 需要增强数据固定，多个组件都需要的话，使用第一种封装，比如用户的信息
> - 需要增强的数据少，比较少的组件需要增强的话，使用第二种封装，

## 3.2 共享context

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755302541000te2l0f.png)


## 3.3 渲染判断鉴权

在开发中，我们可能遇到这样的场景： 

- 某些页面是必须用户登录成功才能进行进入； 
- 如果用户没有登录成功，那么直接跳转到登录页面； 

这个时候，我们就可以使用高阶组件来完成鉴权操作：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755303942000x1tboj.png)
