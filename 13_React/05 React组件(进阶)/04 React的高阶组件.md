# 一、认识高阶组件

高阶函数的维基百科定义：至少满足以下条件之一： 

- 接受一个或多个函数作为输入； 
- 输出一个函数；

JavaScript中比较常见的[[05 数组Array#八、数组的高阶方法|filter、map、reduce]]都是高阶函数。

那么说明是高阶组件是什么呢？ 

- 高阶组件的英文是 Higher-Order Components，简称为 HOC； 
- 官方的定义：高阶组件是参数为组件，<mark class="hltr-cyan">返回值为新组件</mark>的函数；

**可以进行如下的解析**： 

- 首先， 高阶组件 **本身不是一个组件，而是一个函数**； 
- 其次，这个函数的**参数是一个组件**，**返回值也是一个组件**；
- 本质目的是**对传入的组件做一个拦截**，在这个拦截里面可以进行操作。

# 二、高阶组件的定义

高阶组件的调用过程类似于这样：

```jsx
enhance - 增强的
warppeed - 被包裹的

const EnhanceComponent = higherOrderComponent(WarppedComponent)
```

高阶组件的编写·过程类似如下：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755260104000vkbm06.png)

**组件的名称问题**： 

- 在ES6中，类表达式中类名是可以省略的； 

```js
// 类表达式
const Person = class {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}
```

- 组件的名称都可以通过displayName来修改；

> [!tip] 高阶组件并不是React API的一部分，它是基于React的**组合特性而形成的设计模式** 
> 
> 高阶组件在一些React第三方库中非常常见： 
> 
> - 比如redux中的 **connect**；
> - 比如react-router中的 **withRouter**；

# 三、高阶组件的应用

## 3.1 props的增强

![[React高阶组件增强Propos|100%]]

> [!abstract]
> 
> 最终组件的渲染都是在高组件里面进行渲染的，在 App 中组件的实例化本质是实例了高阶组件里面的返回值，所有才说渲染的本质是在高阶组件里面渲染的。

## 3.2 共享context

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755302541000te2l0f.png)


## 3.3 渲染判断鉴权

在开发中，我们可能遇到这样的场景： 

- 某些页面是必须用户登录成功才能进行进入； 
- 如果用户没有登录成功，那么直接跳转到登录页面； 

这个时候，我们就可以使用高阶组件来完成鉴权操作：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755303942000x1tboj.png)

# 四、高阶组件的意义

我们会发现利用高阶组件可以针对某些React代码进行更加优雅的处理。 

其实早期的React有提供组件之间的一种复用方式是mixin，**目前已经不再建议使用**： 

- Mixin 可能会相互依赖，相互耦合，不利于代码维护； 
- 不同的Mixin中的方法可能会相互冲突； 
- Mixin非常多时，组件处理起来会比较麻烦，甚至还要为其做相关处理，这样会给代码造成滚雪球式的复杂性； 

当然，HOC也有自己的一些缺陷： 

- HOC需要在原组件上进行包裹或者嵌套，如果大量使用HOC，将会产生非常多的嵌套，这让调试变得非常困难； 
- HOC可以劫持props，在不遵守约定的情况下也可能造成冲突；

# 五、ref函数组件转发

前面知识点ref时讲过，ref不能应用于函数式组件： 

- 因为函数式组件没有实例，所以不能获取到对应的组件对象 

但是，在开发中我们可能想要获取**函数式组件中某个元素的DOM**，这个时候我们应该如何操作呢？ 

- 方式一：直接传入ref属性（错误的做法） 
- 方式二：通过forwardRef高阶函数,让父组件传入 ref

```jsx
//父组件传入ref到forwordRef的第二个参数
<Home ref={ref} />
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755305639000iwwqtl.png)

那么，如果想要获取到函数组件中的某些方法呢？这个时候就需要使用到 hooks 中的 [[05 useRef和LayoutEffect|useRef]]

