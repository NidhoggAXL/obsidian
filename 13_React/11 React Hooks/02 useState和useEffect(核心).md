# 一、认识useState

State Hook的API就是 useStat,在前面已经进行了学习： 

- useState会帮助我们定义一个 state变量，useState 是一种新方法，它与 class 里面的 this.state 提供的功能完全相同。 
- 一般来说，在函数退出后变量就会”消失”，而 state 中的变量会被 React 保留。
- useState接受唯一一个参数，在**第一次组件被调用时使用来作为初始化值**。（如果没有传递参数，那么初始化值为undefined）。 
- useState的返回值是一个数组，我们可以通过[[05 解构Destructuring#1.1 数组解构|数组的解构]]，来完成赋值会非常方便。
- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring

FAQ：为什么叫 useState 而不叫 createState? 

- “create” 可能不是很准确，因为 state 只在组件首次渲染的时候被创建。 
- **在下一次重新渲染时，useState 返回给我们当前的 state**。 
- 如果每次都创建新的变量，它就不是 “state”了。
- 这也是 Hook 的名字总是以 use 开头的一个原因。

## 1.1 useState基本使用

### 声明状态

```jsx
const [state, setState] = useState(initialValue);
```

### 初始值的不同形式

```jsx
// 直接值
const [count, setCount] = useState(0);

// 函数式初始值（惰性初始化）
const [data, setData] = useState(() => {
  const initialData = localStorage.getItem('data');
  return initialData ? JSON.parse(initialData) : [];
});

// 对象状态
const [user, setUser] = useState({ name: '', age: 0 });
```

## 1.2 更新状态的两种方式

### 直接值更新

```jsx
setCount(10);
setUser({ name: 'John', age: 25 });
```

### 函数式更新

```jsx
setCount(prevCount => prevCount + 1);
setUser(prevUser => ({ ...prevUser, age: 26 }));
```

## 1.3 常见错误及解决方法

### 错误1：直接修改状态对象

```jsx
// ❌ 错误
const [user, setUser] = useState({ name: 'John', age: 25 });
user.age = 26; // 直接修改，不会触发重新渲染

// ✅ 正确
setUser(prevUser => ({ ...prevUser, age: 26 }));
```

### 错误2：连续同步更新

```jsx
// ❌ 错误 - 不会累加
const handleClick = () => {
  setCount(count + 1);
  setCount(count + 1); // 两次都是基于同一个 count 值
};

// ✅ 正确 - 会累加
const handleClick = () => {
  setCount(prev => prev + 1);
  setCount(prev => prev + 1);
};
```

### 错误3：闭包陷阱

```jsx
// ❌ 错误 - 定时器中的 state 不会更新
useEffect(() => {
  const timer = setInterval(() => {
    setCount(count + 1); // 总是使用初始的 count
  }, 1000);
  return () => clearInterval(timer);
}, []);

// ✅ 正确
useEffect(() => {
  const timer = setInterval(() => {
    setCount(prev => prev + 1); // 总是使用最新值
  }, 1000);
  return () => clearInterval(timer);
}, []);
```

### 错误4：异步更新后立即访问状态

```jsx
// ❌ 错误 - 拿不到最新值
const handleClick = () => {
  setCount(100);
  console.log(count); // 还是旧值
};

// ✅ 正确 - 使用 useEffect 监听变化
const handleClick = () => {
  setCount(100);
};
useEffect(() => {
  console.log('count 更新了:', count);
}, [count]);
```

### 错误5：不必要的复杂状态

```jsx
// ❌ 错误 - 过度耦合的状态
const [userData, setUserData] = useState({
  user: null,
  loading: true,
  error: null
});

// ✅ 更好 - 拆分状态
const [user, setUser] = useState(null);
const [loading, setLoading] = useState(true);
const [error, setError] = useState(null);
```

## 1.4 最佳实践

### 使用函数式更新

```jsx
// ✅ 推荐 - 避免闭包问题
setCount(prev => prev + 1);
setUser(prev => ({ ...prev, name: 'Alice' }));
```

### 对象和数组的不可变更新

```jsx
// 对象更新
setUser(prev => ({ ...prev, age: 30 }));

// 数组添加
setItems(prev => [...prev, newItem]);

// 数组删除
setItems(prev => prev.filter(item => item.id !== idToRemove));

// 数组更新
setItems(prev => prev.map(item => 
  item.id === id ? { ...item, completed: true } : item
));
```

### 使用自定义 Hook 封装复杂逻辑

```jsx
function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);
  
  const increment = useCallback(() => setCount(prev => prev + 1), []);
  const decrement = useCallback(() => setCount(prev => prev - 1), []);
  const reset = useCallback(() => setCount(initialValue), [initialValue]);
  
  return { count, increment, decrement, reset };
}

// 使用
const { count, increment } = useCounter(0);
```

## 1.5 性能优化技巧

### 使用 useCallback 避免不必要的重新渲染

```jsx
const increment = useCallback(() => {
  setCount(prev => prev + 1);
}, []);
```

### 惰性初始状态

```jsx
// 对于昂贵的计算，使用函数式初始值
const [data, setData] = useState(() => {
  return expensiveCalculation(props);
});
```

### 使用 [[04 useCallback和useMemo|useMemo]] 优化派生状态

```jsx
const expensiveValue = useMemo(() => {
  return items.filter(item => item.active).length;
}, [items]);
```

## 1.6 总结要点

1. **状态更新是异步的** - 不要指望立即拿到新值
    
2. **使用函数式更新**解决依赖前状态的更新问题
    
3. **保持状态不可变** - 总是返回新对象/数组
    
4. **合理拆分状态** - 避免过度耦合的状态对象
    
5. **注意闭包陷阱** - 在 useEffect、useCallback 中特别注意
    
6. **性能优化** - 使用 useCallback、useMemo 避免不必要的计算和渲染


# 二、认识Effect Hook

目前已经通过hook在函数式组件中定义state，那么类似于生命周期这些呢？ 

- Effect Hook 可以让你来完成一些类似于class中[[02 React组件生命周期|生命周期]]的功能； 
- 事实上，类似于**网络请求、手动更新DOM、一些事件的监听**，都是React更新DOM的一些**副作用（Side Effects**）； 
- 所以对于完成这些功能的Hook被称之为 **Effect Hook**； 

**假如我们现在有一个需求**：页面的title总是显示counter的数字，使用Hook实现：

```jsx
import React, { memo, useEffect, useState } from 'react'

const App = memo(() => {
  const [count, setCount] = useState(200)

  useEffect(() => {
    document.title = count
  })

  return (
    <div>
      <h2>App</h2>
      <button onClick={e => setCount(count+1)}>+1</button>
    </div>
  )
})

export default App
```

useEffect的解析： 

- 通过useEffect的Hook，可以告诉React需要在渲染后执行某些操作； 
- useEffect要求我们传入一个回调函数，在**React执行完更新DOM操作之后（render）**，就会回调这个函数； 
- 默认情况下，**无论是第一次渲染之后，还是每次更新之后**，都会执行这 **回调函数**；

# 三、需要清除Effect

在class组件的编写过程中，某些副作用的代码，需要在 [[02 React组件生命周期#2.3 常用生命周期|componentWillUnmount]] 中进行清除： 

- 比如我们之前的[[06 自定义事件总线|事件总线]]或Redux中手动调用 [[02 Redux的使用#^de6d55|subscribe]]； 
- 都需要在componentWillUnmount有对应的取消订阅； 
- Effect Hook通过什么方式来模拟componentWillUnmount呢？

useEffect传入的**回调函数A**本身可以有一个返回值，这个返回值是另外一个**回调函数B**：

```ts
type EffectCallback = () => (void | (() => void | undefined));
```

为什么要在 effect 中返回一个函数？ 

- 这是 effect 可选的清除机制。**每个 effect 都可以返回一个清除函数**； 
- 如此可以将**添加和移除订阅的逻辑放在一起**； 
- 它们都属于 effect 的一部分； 

React 何时清除 effect？ 

- React 会在组件**更新和卸载**的时候执行清除操作； 
- 正如之前学到的，effect 在每次渲染的时候都会执行；

```jsx
import React, { memo, useEffect, useState } from 'react'

const App = memo(() => {
  const [count, setCount] = useState(200)

  useEffect(() => {
    console.log("一些副作用代码的监听")
    return () => {
      console.log("取消副作用代码的监听")
    }
  })

  return (
    <div>
      <h2>App</h2>
      <button onClick={e => setCount(count+1)}>+1</button>
    </div>
  )
})

export default App
```

如果点击按钮让函数组件重新渲染执行后的打印结果如下：

```text
一些副作用代码的监听
取消副作用代码的监听
一些副作用代码的监听
```

# 四、使用多个Effect

使用Hook的其中一个目的就是解决class中生命周期经常将很多的逻辑放在一起的问题： 

- 比如**网络请求、事件监听、手动修改DOM**，这些往往都会放在 [[02 React组件生命周期#2.3 常用生命周期|componentDidMount]] 中； 

使用Effect Hook，我们可以将它们分离到不同的useEffect中：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17557612390006vxnlx.png)

> [!tip] 使用：
> **Hook 允许我们按照代码的用途分离它们**， 而不是像生命周期函数那样： 
> React 将按照 **effect 声明的顺序依次调用**组件中的每一个 effect；

# 五、Effect性能优化

默认情况下，**useEffect的回调函数会在每次渲染时都重新执行**，但是这会导致两个问题： 

- 某些代码我们只是希望执行一次即可，类似于 **componentDidMount** 和 **componentWillUnmount** 中完成的事情；（比如网络请求、订阅和取消订阅）； 
- 另外，多次执行也会**导致一定的性能问题**；

如何决定useEffect在什么时候应该执行和什么时候不应该执行呢？ 

- useEffect实际上有两个参数： 
- **参数一**：执行的回调函数； 
- **参数二**：该useEffect在哪些**state发生变化**时，**才重新执行**；（**受谁的影响**） 

**案例练习**：  受count影响的Effect； 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755761768000wtj1zw.png)


但是，如果一个函数我们不希望依赖任何的内容时，也可以传入一个**空的数组`[]`**： 

- 那么这里的两个回调函数分别对应的就是componentDidMount和componentWillUnmount生命周期函数了；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175576186000015j1ps.png)



