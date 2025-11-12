# 一、认识CSS in JS

官方文档也有提到过CSS in Js这种方案:

- “CSS-in-JS”是指一种模式，其中 **CSS 由JavaScript 生成而不是在外部文件中定义**;
- 注意此功能并不是 React 的一部分，而是由第三方库提供;
- React 对样式如何定义并没有明确态度;

在传统的前端开发中，我们通常会将结构（HTML）、样式（CSS）、逻辑（JavaScript）进行分离。 

- 但是在前面的知识中，就提到过，React的思想中认为逻辑本身和UI是无法分离的，所以才会有了JSX的语法。 
- 样式呢？**样式也是属于UI的一部分**； 
- 事实上CSS-in-JS的模式就是一种**将样式（CSS）也写入到JavaScript中的方式**，并且可以方便的使用JavaScript的状态； 
- 所以React有被人称之为 **All in JS**； 

当然，这种开发的方式也受到了很多的批评：

- Stop using CSS in JavaScript for web development 
- https://hackernoon.com/stop-using-css-in-javascript-for-web-development-fa32fb873dcc

# 二、认识styled-components

批评声音虽然有，但是在我们看来很多优秀的CSS-in-JS的库依然非常强大、方便： 

- CSS-in-JS通过JavaScript来为CSS赋予一些能力，包括类似于**CSS预处理器**一样的样式**嵌套、函数定义、逻辑复用、动态修改**状态等等； 
- 虽然CSS预处理器也具备某些能力，但是获取动态状态依然是一个不好处理的点； 
- 所以，目前可以说CSS-in-JS是React编写CSS最为受欢迎的一种解决方案； 

目前比较流行的CSS-in-JS的库有哪些呢？ 

- styled-components 
- emotion 
- glamorous 

目前可以说styled-components依然是社区最流行的CSS-in-JS库，所以我们以styled-components的讲解为主；

安装styled-components：

```bash
yarn add styled-components
```

# 三、ES6标签模板字符串

ES6中增加了[[04 模板字符串的详解|模板字符串]]的语法，这个对于很多人来说都会使用。 

但是模板字符串还有另外一种用法：**标签模板字符串（Tagged Template Literals）。**

我们一起来看一个普通的JavaScript的函数： 

- 正常情况下，我们都是通过 函数名() 方式来进行调用的，其实函数还有另外一种 调用方式： 

```js
function foo(...args) {
  console.log(args)
}

//基本调用
foo('hello world')
// 模板字符串
foo`hello world`

const name = '雷姆'
const song = 'ai'
foo`hello world ${name}, good ${song}`
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755344911000l7se8y.png)


如果我们在调用的时候插入其他的变量： 

- 模板字符串被拆分了； 
- 第一个元素是数组，是被模块字符串拆分的字符串组合； 
- 后面的元素是一个个模块字符串传入的内容；

**在styled component中，就是通过这种方式来解析模块字符串，最终生成我们想要的样式的**

# 四、styled的基本使用

为了获得更好的styled components的代码提示可以下载插件：vscode-styled-components

![gh|400](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755345362000ju26xx.png)


styled-components的本质是通过函数的调用，最终创建出一个组件： 

- 这个组件会被自动添加上一个不重复的class； 
- styled-components会给该class添加相关的样式；

另外，它**支持类似于CSS预处理器一样的样式嵌套**： 

- 支持直接子代选择器或后代选择器，并且直接编写样式； 
- 可以**通过&符号获取当前元素**； 
- 直接[[09 伪类选择器|伪类选择器]]、[[10 伪元素（pseudo-elements）|伪元素]]等；

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755345591000u1v2cp.png)

```jsx
import React, { PureComponent } from 'react'
import { styled } from 'styled-components'

const AppWarpper = styled.div`
  .title {
    font-size: 24px;
    color: red;
  }
  .list {
    border: 1px solid red;
    .item {
      height: 20px;
      background-color: skyblue;

      &:hover{
        font-size: 18px;
        background-color: orange;
      }
    }
  }
`

export class App extends PureComponent {
  render() {
    return (
      <AppWarpper>
        <div className="title">我是标题</div>
        <ul className="list">
          <li className="item">大话西游</li>
          <li className="item">大话西游</li>
          <li className="item">大话西游</li>
          <li className="item">大话西游</li>
        </ul>
      </AppWarpper>
    )
  }
}

export default App
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755345638000ejtlw8.png)

# 五、props、attrs属性

props可以传递：

```jsx
<HYInput type="password" $left="20px" />
```

> [!warning] 
> 
> 非标准的属性（`left` 和 `paddingLeft`）传递给了底层的 DOM `<input>` 元素。React 会警告你这些属性不是有效的 DOM 属性。解决方案是使用 **临时属性**（transient props），即在属性名前加 `$` 符号，这样 styled-components 就知道这些属性只用于样式计算，不会传递给 DOM。

props可以被传递给styled组件 

- 获取props需要通过 **`${}`** 传入一个**插值函数**，props会作为该函数的参数； 
- 这种方式可以有效的解决动态样式的问题；

attrs属性可以设置**默认参数**：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755349302000jx6l7e.png)


> [!warning] 
> 
> 注意 $paddingLeft 属性名不可以编写为 $left ，不然会造成错误，形成死亡回调
> `Uncaught RangeError: Maximum call stack size exceeded`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175534943500052iaxf.png)

# 六、styled高级特性

styled设置主题：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755350333000yve19w.png)

支持样式的继承：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755351111000y6ueol.png)






