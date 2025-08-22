# 一、useRef

useRef返回一个ref对象，<mark class="hltr-orange">返回的ref对象在组件的整个生命周期保持不变</mark>。 

最常用的ref是两种用法： 

- 用法一：引入DOM（或者组件，但是需要是class组件）元素； 
- 用法二：保存一个数据，这个对象在整个生命周期中可以保存不变；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755782413000pj9b2d.png)

- 案例一：引用DOM，获取input的DOM，并获取焦点 

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755782828000mgnmzh.png)

- 案例二：使用ref保存上一次的某一个值，不管点击多少次按钮都是{current: 100}

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755783174000vjhpaw.png)

## 1.1 useImperativeHandle

先来回顾一下ref和forwardRef结合使用： 

- 通过 [[04 React的高阶组件#五、ref转发|forwardRef]] 可以将ref转发到子组件； 
- 子组件拿到父组件中创建的ref，绑定到自己的某一个元素中； 

forwardRef的做法本身没有什么问题，但是我们是将子组件的DOM直接暴露给了父组件： 

- 直接**暴露给父组件带来的问题是某些情况的不可控**； 
- 父组件可以拿到DOM后进行任意的操作； 
- 但是，事实上在上面的案例中，我们只是**希望父组件可以操作的focus**，其他并不希望它随意操作；

![gh|650](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755785551000cha4o8.png)

通过useImperativeHandle可以值暴露固定的操作： 

- 通过useImperativeHandle的Hook，将传入的ref和useImperativeHandle第二个参数返回的对象绑定到了一起； 
- 所以在父组件中，使用 inputRef.current时，**实际上使用的是返回的对象**； 
- 比如我调用了 **focus函数**

# 二、useLayoutEffect

useLayoutEffect看起来和useEffect非常的相似，事实上他们也只有一点区别而已：

- useEffect会在渲染的内容更新到DOM上后执行，不会阻塞DOM的更新； 
- useLayoutEffect会在渲染的**内容更新到DOM上之前执行**，**会阻塞DOM的更新**；
- `useLayoutEffect` 是 [`useEffect`](https://zh-hans.react.dev/reference/react/useEffect) 的一个版本，在浏览器重新绘制屏幕之前触发。

如果我们希望在某些操作发生之后再更新DOM，那么应该将这个操作放到useLayoutEffect。

> [!warning] `useLayoutEffect` 可能会影响性能。尽可能使用 [`useEffect`](https://zh-hans.react.dev/reference/react/useEffect)。

```jsx
useLayoutEffect(setup, dependencies?)
```

```jsx
function Tooltip() {
  const ref = useRef(null);
  const [tooltipHeight, setTooltipHeight] = useState(0); // 你还不知道真正的高度

  useLayoutEffect(() => {
    const { height } = ref.current.getBoundingClientRect();
    setTooltipHeight(height); // 现在重新渲染，你知道了真实的高度
  }, []);

  // ... 在下方的渲染逻辑中使用 tooltipHeight ...
}
```

案例： useEffect和useLayoutEffect的对比

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755820133000xlg3a9.png)
