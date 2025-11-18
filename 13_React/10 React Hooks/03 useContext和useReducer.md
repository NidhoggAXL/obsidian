# 一、useContext的使用

在之前的开发中，我们要在组件中使用共享的[[04 React的高阶组件#3.2 共享context|Context]]有两种方式： 

- 类组件可以通过 **类名.contextType = MyContext** 方式，在类中获取context； 
- 多个Context或者在函数式组件中通过 **MyContext.Consumer** 方式共享context；

但是多个Context共享时的方式会存在大量的嵌套：  Context Hook允许我们**通过Hook来直接获取某个Context的值**；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755765139000lya45d.png)

> [!warning] 注意事项： 
>  当组件上层最近的 `<MyContext.Provider>` 更新时，该 Hook 会触发重新渲染，并使用最新传递给 MyContext provider 的 context value 值。 

# 二、useReducer

很多人看到useReducer的第一反应应该是[[02 Redux的使用|redux]]的某个替代品，其实并不是。 

useReducer仅仅是[[02 State和Effect(核心)|useState]]的一种替代方案： 

- 在某些场景下，如果state的处理逻辑比较复杂，我们可以通过useReducer来对其进行拆分； 
- 或者这次**修改的state需要依赖之前的state时**，也可以使用；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175576601500085vxbk.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755766024000a8jq5a.png)

> [!note] 
> 数据是不会共享的，它们只是使用了相同的counterReducer的函数而已。 
> 所以，useReducer只是useState的一种替代品，并不能替代Redux。

