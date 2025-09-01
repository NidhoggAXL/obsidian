
# 一、Redux测试项目搭建

安装redux：

```bash
npm install redux --save 
# 或 
yarn add redux
```

1. 创建一个新的项目文件夹：learn-redux

```bash
# 执行初始化操作
yarn init
# 安装redux
yarn add redux
```

2. 创建src目录，并且创建index.js文件

3. 修改package.json可以执行index.js

```bash
"scripts": {
	"start": "node src/index.js"
}
```

# 二、Redux的使用过程

1. 创建一个对象，作为我们要保存的状态： 
2. 创建Store来存储这个state 
	- 创建store时必须创建reducer； 
	- 我们可以通过 store.getState 来获取当前的state；
3. 通过action来修改state 
	- 通过dispatch来派发action； 
	- 通常action中都会有type属性，也可以携带其他的数据； 
4. 修改reducer中的处理代码 
	- 这里一定要记住，**reducer是一个纯函数，不需要直接修改state；** 
	- 后面我会讲到直接修改state带来的问题a
5. 可以在派发action之前，监听store的变化：

```js
const { createStore } = require("redux")

const initState = {
  name: 'axl',
  age: 18
}

function reduex(state = initState, action) {
  switch(action.type) {
    case 'change_name':
      return { ...state, name: action.name }
    case "change_age":
      return { ...state, age: 19 }
    default:
      return state
  }
}

const store = createStore(reduex)

console.log(store.getState())
//{ name: 'axl', age: 18 }

store.dispatch({ type: 'change_name', name: '雷姆' })
store.dispatch({ type: 'change_age', age: 19 })

console.log(store.getState())
//{ name: '雷姆', age: 19 }

```

# 三、Redux结构划分

如果我们将所有的逻辑代码写到一起，那么当redux变得复杂时代码就难以维护。 接下来，我会对代码进行拆分，将store、reducer、action、constants拆分成一个个文件。 

- 创建store/index.js文件： 
- 创建store/reducer.js文件： 
- 创建store/actionCreators.js文件： 
- 创建store/constants.js文件：

![[Redux目录结构|100%]]


调用：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755396668000hgylzs.png)

> 每次改变如果都需要知道改变了那些值，都需要打印的话太麻烦，可以使用`store.subscribe(() => console.log(store.getState()))`订阅来查看改变了。

> [!tip] 注意：node中对ES6模块化的支持 
> 
> - 目前我使用的node版本是v12.16.1，从node v13.2.0开始，node才对ES6模块化提供了支持： 
> - node v13.2.0之前，需要进行如下操作： 
> 	- 在package.json中添加属性： "type": "module"； 
> 		- 在执行命令中添加如下选项：node --experimental-modules src/index.js; 
> 	- node v13.2.0之后，只需要进行如下操作： 
> 		- 在package.json中添加属性： "type": "module"； 

>[!node] 注意：导入文件时，需要跟上.js后缀名；

# 四、Redux使用流程

我们已经知道了redux的基本使用过程，那么我们就更加清晰来认识一下redux在实际开发中的流程：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755397763000xkhwsj.png)

# 五、Redux官方图

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755397776000m94qjn.png)


