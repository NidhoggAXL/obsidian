# 一、React开发依赖

开发React必须依赖三个库： 

- **react**：包含react所必须的核心代码 
- **react-dom**：react渲染在不同平台所需要的核心代码 
- **babel**：将jsx转换成React代码的工具 


第一次接触React会被它繁琐的依赖搞蒙，居然依赖这么多东西： 

- 对于Vue来说，我们只是依赖一个vue.js文件即可，但是react居然要**依赖三个包**。 
- 其实呢，这三个库是各司其职的，目的就是让每一个库只**单纯做自己的事情**; 
- 在**React的0.14版本之前是没有react-dom这个概念**的，所有功能都包含在react里；

为什么要进行拆分呢？**原因就是react-native**。 

- react包中包含了react-web和react-native所共同拥有的核心代码。 
- **react-dom**针对web和native所**完成的事情不同**： 
	- web端：react-dom会将jsx最终渲染成真实的DOM，显示在浏览器中 
	- native端：react-dom会将jsx最终渲染成**原生的控件**（比如Android中的Button，iOS中的UIButton）。

# 二、Babel和React的关系

babel是什么呢？

- Babel ，又名 Babel.js。 
- 是目前前端使用非常广泛的**编译器、转移器**。 
- 比如当下很多浏览器并不支持ES6的语法，但是确实ES6的语法非常的简洁和方便，我们开发时希望使用它。 
- 那么编写源码时我们就可以使用ES6来编写，之后通过Babel工具，将ES6转成大多数浏览器都支持的ES5的语法。

React和Babel的关系： 

- 默认情况下开发React其实**可以不使用babel**。 
- 但是前提是我们自己使用 React.createElement 来编写源代码，它编写的代码非常的繁琐和可读性差。 
- 那么我们就可以直接编写jsx（JavaScript XML）的语法，并且让babel帮助我们转换成React.createElement。 

# 三、React的依赖引入

如何添加这三个依赖： 

- 方式一：直接CDN引入 
- 方式二：下载后，添加本地依赖 
- 方式三：通过npm管理（后续脚手架再使用）

暂时直接通过CDN引入，来演练下面的示例程序： 

- 这里有一个**crossorigin的属性**，这个属性的**目的是为了拿到跨域脚本的错误信息**

```html
  <!-- React 核心库 -->
  <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
  
  <!-- ReactDOM 库（用于 DOM 操作） -->
  <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
  
  <!-- Babel（用于浏览器端编译 JSX） -->
  <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```

# 四、Hello World

第一步：在界面上通过React显示一个Hello World 

- 注意：这里我们编写React的script代码中，**必须添加 type="text/babel"**，作用是可以让babel解析jsx的语法

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754816156000i8ur5o.png)

ReactDOM. createRoot函数：用于创建一个React根，之后渲染的内容会包含在这个根中 

- 参数：将渲染的内容，挂载到哪一个HTML元素上  
	- 这里我们已经提定义一个id为app的div 

root.render函数: 

- 参数：要渲染的根组件 

我们可以通过 **{}语法** 来引入外部的变量或者表达式

**现在添加一个按钮，通过按钮来改变内容：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17548164490008u9h7b.png)


