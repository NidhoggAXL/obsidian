# 一、useCallback

useCallback实际的目的是为了进行性能的优化。 

如何进行性能的优化呢？ 

- useCallback会返回一个**函数的 memoized（记忆的）** 值； 
- 在`[]`依赖不变的情况下，多次定义的时候，返回的值是相同的；

## 1.1 闭包陷阱

先看下面的代码：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755773045000ywt73n.png)

[[03 闭包#一、闭包的定义|闭包]]在函数被定义的时候就以及形成啦，那么这个时候 `setCount(count + 2)`通过闭包查询到上层作用域的 count 为 0 ，当点击的时候调用 addCount 后 count + 2 = 2

当再次点击的时候因为 useCallback 的第二参数，没有依赖返回的值是相同的，那么还是上一个函数(**同一个函数**)，而上一个函数依赖的 count 还是 0， 所以页面显示是 2.

## 1.2 优化使用场景

通常使用useCallback的目的是**不希望子组件进行多次渲染**，并不是为了函数进行缓存；

![gh|70%](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17557755850005ko20s.png)

> [!tip] 函数组件是否渲染，跟父组件是否渲染以及props是否改变有关

如果还希望，**当子组件点击的时候也还是不进行渲染**，那么可以使用 [[05 Ref和LayoutEffect|useRef]]：这样useCallback放回的还是用一个函数，但是函数内部改变了count。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755777948000l5e4vf.png)

# 二、useMemo

useMemo实际的目的也是为了进行性能的优化。 

如何进行性能的优化呢？ 

- useMemo返回的也是一个 **memoized（记忆的）值**； 
- 在依赖不变的情况下，多次定义的时候，<mark class="hltr-orange">返回的值是相同的</mark>；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755780514000zq74z9.png)

## 2.1 案例一

进行大量的计算操作，是否有必须要每次渲染时都重新计算； 

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755781178000gmdzm4.png)

> [!note] 这样当点击的时候，sum没有依赖任何东西，那么就不会对 sumAll 的计算操作(和自身的state无关)重复操作

## 2.2 案例二

对子组件传递**相同内容的对象**时，使用useMemo进行性能的优化

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755781618000eob58c.png)

对象的每一次定义，不管内容是什么都是不同的对象：

```jsx
function obj() {
  return {name: 'axl'}
}

console.log(obj()===obj())//false
```

