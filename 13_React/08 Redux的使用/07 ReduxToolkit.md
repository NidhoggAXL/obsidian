# 一、认识Redux Toolkit

Redux Toolkit 是官方推荐的编写 Redux 逻辑的方法。 

- 在前面学习Redux的时候应该已经发现，redux的编写逻辑过于的繁琐和麻烦。 
- 并且代码通常分拆在多个文件中（虽然也可以放到一个文件管理，但是代码量过多，不利于管理）； 
- Redux Toolkit包旨在成为编写Redux逻辑的标准方式，从而解决上面提到的问题； 
- 在很多地方为了称呼方便，也将之称为“RTK”； 

安装Redux Toolkit：

```bash
	npm install @reduxjs/toolkit react-redux
```

**Redux Toolkit的核心API主要是如下几个：** 

- **configureStore**：包装createStore以提供简化的配置选项和良好的默认值。它可以自动组合你的 slice reducer，添加你提供 的任何 Redux 中间件，**redux-thunk默认包含，并启用 Redux DevTools Extension**。 
- **createSlice**：接受reducer函数的对象、切片名称和初始状态值，并自动生成切片reducer，并带有相应的actions。 
- **createAsyncThunk**: 接受一个动作类型字符串和一个返回承诺的函数，并生成一个pending/fulfilled/rejected基于该承诺分 派动作类型的 thunk

# 二、创建counter的reducer

我们先对counter的reducer进行重构： 通过createSlice创建一个slice。 

**createSlice主要包含如下几个参数：**

- **name**：用户标记slice的名词 
	- 在之后的redux-devtool中会显示对应的名词； 
- **initialState**：初始化值 
	- 第一次初始化时的值；
- **reducers**：相当于之前的reducer函数 
	- 对象类型，并且可以添加很多的函数； 
	- 函数类似于redux原来reducer中的一个case语句； 
	- 函数的参数：
		- 参数一：state
		- 参数二：调用这个action时，传递的action参数
	- 在这里可以直接修改 state，但是**内部会自动处理这个直接修改，让其变成不是直接对state修改**。
- <mark class="hltr-orange">createSlice返回值是一个对象，包含所有的actions</mark>

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755648797000ly3bh5.png)

# 三、创建categories的reducer

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175564884600015a704.png)

# 四、store的创建

configureStore用于创建store对象，常见参数如下： 

- **reducer**，将slice中的reducer可以组成一个对象传入此处； 
- **middleware**：可以使用参数，传入其他的中间件（自行了解）； 
- **devTools**：是否配置[[05 redux-devtool|devTools]]工具，默认为true；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755648989000b2tmvo.png)


# 五、Redux Toolkit的异步操作

在之前的开发中，我们通过redux-thunk中间件让dispatch中可以进行异步操作。 

Redux Toolkit默认已经给我们继承了Thunk相关的功能：createAsyncThunk

- payload接收其他参数
- extraInfo接收一个store，里面包含了dispatch、getState，可以通过结构获取

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755656559000lh157h.png)


当createAsyncThunk创建出来的action被dispatch时，会存在三种状态：

- **pending(待处理)**：action被发出，但是还没有最终的结果； 
- **fulfilled(已完成)**：获取到最终的结果（有返回值的结果）； 
- **rejected(被拒绝**)：执行过程中有错误或者抛出了异常；

可以在createSlice的extraReducer中监听这些结果：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17556567410004vvyl7.png)

