在之前的redux开发中，为了让组件和redux结合起来，我们使用了react-redux中的connect： 

- 但是这种方式必须使用高阶函数结合返回的高阶组件； 
- 并且必须编写：mapStateToProps和 mapDispatchToProps映射的函数； 

在Redux7.1开始，提供了Hook的方式，我们再也不需要编写connect以及对应的映射函数了


**useSelector** 的作用是将state映射到组件中： 

- 参数一：将state映射到需要的数据中； 
- 参数二：可以进行比较来决定是否组件重新渲染；


**useSelector** 默认会比较我们返回的两个对象是否相等； 

- 如何比较呢？ const refEquality = (a, b) => a === b； 
- 也就是我们必须返回两个完全相等的对象才可以不引起重新渲染；

先来看两个使用：

```jsx
//返回对象(错误使用)
//这种写法会导致每次组件渲染时都创建一个新的对象，即使 `state.counter.count` 的值没有变化。
const { count } = useSelector((state) => ({ count: state.counter.count }))
//直接返回数值(正确使用)
const count = useSelector(state => state.counter.count)
```

> [!warning] 警告
> **Redux 更新机制**：当 Redux store 更新时，所有 `useSelector` 钩子都会重新执行
> 
> 如果每次返回的都是不同的对象，这样的话不管count有没有发生改变都会渲染，特别是如果存在子组件的时候，子组件改变父组件也会改变
> 


**尽量不要useSelector返回一个对象**,如果非要放回一个对象的话需要使用 useSelector 的第二个参数。

```jsx
import { shallowEqual, useSelector } from 'react-redux';

// 使用浅比较作为第二个参数
const { count } = useSelector(
  state => ({ 
    count: state.counter.count
  }),
  shallowEqual // 使用浅比较而不是引用比较
);
```

**useDispatch非常简单，就是直接获取dispatch函数，之后在组件中直接使用即可；** 

**还可以通过useStore来获取当前的store对象；**


![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17558330960008s6zc5.png)



