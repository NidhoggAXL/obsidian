# 一、如何使用Pinia

使用Pinia之前，我们需要先对其进行安装：

```bash
yarn add pinia
npm install pinia
```

创建一个pinia并且将其传递给应用程序

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748006911000618tgf.png)

# 二、认识Store

什么是Store?

- 一个 store (如 Pinia)是一个实体，它会**持有为绑定到你组件树的状态和业务逻辑**，也就是保存了全局的状态,
- 它有点像始终存在，并且每个人都可以读取和写入的组件
- 你可以在你的应用程序中定义任意数量的store来管理你的状态，

store有三个核心概念:

- state、getters、 actions;
- 等同于组件的data、computed、methods;
- 一旦 store 被实例化，你就可以直接在 store 上访问 state、getters 和 actions 中定义的任何属性;


# 三、定义一个Store

定义一个Store： 

* 需要知道 **Store 是使用 defineStore() 定义的**，
* 并且它需要一个唯一名称，作为第一个参数传递（类似ID）；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748007139000hte7hk.png)

## defineStore的返回值

 **defineStore 返回的是一个函数**，这也是 composition API 方便使用的原因。上面的 counter，也称为 id，是必要的，Pinia 使用它来将 store 连接到 devtools。

> [!abstract] 
> 
> 返回的函数统一使用useX作为命名方案，这是约定的规范；use + name 使用小驼峰命名

当 Store 要使用其他 Store 的 [[04 Pinia核心概念Getters#^0c656b|state、getters、actiongs]] 的时候，就更加的具有通用性

**这种设计的好处：**

- **延迟初始化**: Store 只在第一次调用时创建
    
- **单例模式**: 多次调用返回同一个实例
    
- **Composition API 友好**: 符合 Vue 3 的函数式风格
    
- **类型安全**: 完整的 TypeScript 支持


# 四、使用定义的Store

Store在它被使用之前是不会创建的，可以通过**调用use函数来使用Store**：

* 使用的时候不需要再确定使用 counter 里面的什么属性（`counter.state.count`)，直接使用就可以啦（`counter.count`)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17480082080005nwf7p.png)

> [!warning]
> 
> 注意Store获取到后不能被解构，那么会失去响应式： 为了从 Store 中提取属性同时保持其响应式，需要使用storeToRefs()。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748008826000rs9p8r.png)

