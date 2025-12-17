# 一、认识Redux Toolkit（RTK）

Redux Toolkit 是官方推荐的编写 Redux 逻辑的方法。

 - 以前我们在使用redux的时候，通常会将redux代码拆分在多个文件中，比如：constants、action、reducer 等
 - 这种代码组织方式过于繁琐和麻烦，导致代码量过多，也不利于后期管理
 - Redux Toolkit 就是为了**解决这种编码方式而诞生。**
 - **并且以前的 createStore 方式已标为过时，而 Redux Toolkit 已成为官方推荐**；

安装Redux Toolkit：

```bash
npm install @reduxjs/toolkit react-redux
```

Redux Toolkit的核心API主要是如下几个：

 - **configureStore**：包装createStore以提供简化的配置选项和良好的默认值。
	 - **可自动组合 slice reducer**
	 - 可添加其它 Redux 中间件，redux-thunk默认包含，
	 - 默认启用 Redux DevTools Extension
 - **createSlice**：接受切片名称、初始状态值和reducer函数的对象，并自动生成切片reducer，并带有相应的actions。
 - **createAsyncThunk**: 接受一个动作类型字符串和一个返回承诺的函数，并生成一个pending/fulfilled/rejected基于该承诺分派动作类型的thunk。简单理解就是专门用来创建异步Action。

# 二、创建reducer模块

创建counter模块的reducer： 通过createSlice创建一个slice。

createSlice主要包含如下几个参数：

 - name：用来标记slice的名词
	 - **redux-devtool中会显示对应的名词；**
 - initialState：第一次初始化时的值；
 - reducers：相当于之前的reducer函数
	 - 对象类型，并且可以添加很多的函数；
	 - 函数类似于redux原来reducer中的一个case语句；
	 - 函数的参数
		 - 参数一：stat
		 - 参数二：action
 - createSlice 返回值是一个对象
	 - 对象包含所有的 actions 和 reducer；


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765955836000gpjk45.png)

# 三、store创建

configureStore用于创建store对象，常见参数如下：

 - reducer，将slice中的reducer可以组成一个对象传入此处；
 - middleware：可以使用参数，传入其他的中间件（自行了解）；
 - devTools：是否配置devTools工具，默认为true；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765955894000o26u2t.png)

# 四、store接入应用

在app.js中将store接入应用：

 - Provider，内容提供者，给所有的子或孙子组件提供store对象；
 - store： 使用configureStore创建的store对象；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765955938000pxzlyu.png)


# 五、开始使用store

在函数式组件中可以使用 react-redux 提供的 Hooks API 连接、操作 store。

 - useSelector 允许你使用 selector 函数从 store 中获取数据（root state）。
 - useDispatch 返回 redux store 的 dispatch 引用。你可以使用它来 dispatch actions。
 - useStore 返回一个 store 引用，和 Provider 组件引用完全一致。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17659560110000bi1kr.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765956019000ucn5cy.png)


# 六、Redux Toolkit异步Action操作

在之前的开发中，我们通过redux-thunk中间件让dispatch中可以进行异步操作。

Redux Toolkit默认已经给我们继承了Thunk相关的功能：createAsyncThunk

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765956040000o5wr2o.png)


当createAsyncThunk创建出来的action被dispatch时，会存在三种状态：

 - pending：action被发出，但是还没有最终的结果；
 - fulfilled：获取到最终的结果（有返回值的结果）；
 - rejected：执行过程中有错误或者抛出了异常；

我们可以在createSlice的entraReducer中监听这些结果：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17556567410004vvyl7.png)

