# 一、布局

每一个页面都可以在同目录下面创建 layout.tsx 布局文件，如果同目录下面没有就会向上层查找。

> [!tip] 
> 根目录下面 layout.tsx 是必须有的，所以不会存在找不到布局文件
> **布局可以进行嵌套：本目录布局文件被上一层布局文件包裹**

![gh|300](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774595249000vptup5.png)

# 二、组件生命周期

|         组件类型         | 执行环境 | 生命周期执行情况                                                                                                                                                                                                                                                                                                                                                                                        |
| :------------------: | ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|   Server Component   | 服务器端 | **不执行任何生命周期方法**（包括 `useEffect`、`componentDidMount` 等）。  <br>只执行纯渲染逻辑和异步数据获取（`async/await`）[](https://nextjscn.org/docs/app/getting-started/server-and-client-components#examples)[](https://nextjs.org/docs/app/getting-started/server-and-client-components?utm_source=slothbytes.beehiiv.com&utm_medium=referral&utm_campaign=react-server-components-for-dummies)。                           |
|                      | 客户端  | **不执行**。代码不会被打包发送给浏览器 [](https://nextjscn.org/docs/app/getting-started/server-and-client-components#examples)[](https://nextjs.org/docs/app/getting-started/server-and-client-components?utm_source=slothbytes.beehiiv.com&utm_medium=referral&utm_campaign=react-server-components-for-dummies)。                                                                                               |
| **Client Component** | 服务器端 | **只执行预渲染**（生成静态 HTML），执行 `render` 方法。  <br>**不执行** `useEffect` 或 `componentDidMount`（因为此时 DOM 还不存在）[](https://nextjscn.org/docs/app/getting-started/server-and-client-components#examples)[](https://nextjs.org/docs/app/getting-started/server-and-client-components?utm_source=slothbytes.beehiiv.com&utm_medium=referral&utm_campaign=react-server-components-for-dummies)。                  |
|                      | 客户端  | **执行完整生命周期**。  <br>1. 首次加载：执行水合（hydration）[](https://nextjscn.org/docs/app/getting-started/server-and-client-components#examples)[](https://nextjs.org/docs/app/getting-started/server-and-client-components?utm_source=slothbytes.beehiiv.com&utm_medium=referral&utm_campaign=react-server-components-for-dummies)。  <br>2. 挂载后：执行 `useEffect` 或 `componentDidMount`。  <br>3. 更新/卸载：执行正常生命周期。 |


### 🖥️ 服务器端执行细节

在 Next.js 的服务器端渲染流程中：

1. **Server Components 直接执行**
    
    - 它们被渲染成一种叫做 **React Server Component Payload (RSC Payload)** 的紧凑数据格式 。
        
    - **关键点**：在这里，你**不能**使用 `useState`、`useEffect` 或任何类组件的生命周期方法。它们只负责获取数据并输出 UI 结构。
        
2. **Client Components 预渲染 HTML**
    
    - Next.js 也会在服务器上执行 Client Components，但只是运行它们的 `render` 方法（或函数组件的函数体），生成静态的 HTML 字符串 [](https://nextjscn.org/docs/app/getting-started/server-and-client-components#examples)[](https://nextjs.org/docs/app/getting-started/server-and-client-components?utm_source=slothbytes.beehiiv.com&utm_medium=referral&utm_campaign=react-server-components-for-dummies)。
        
    - **注意**：在这个阶段，即使你在 Client Component 中写了 `useEffect(() => {...}, [])`，它**不会**在服务器上执行。类组件的 `componentDidMount` 同样不会被调用。


### 🌐 客户端执行细节

当浏览器接收到 HTML 和 JavaScript 后，发生以下过程：

1. **首次加载：水合**
    
    - 这是 React 在客户端将事件处理程序附加到现有 HTML 上的过程，使页面变得可交互 [](https://nextjscn.org/docs/app/getting-started/server-and-client-components#examples)[](https://nextjs.org/docs/app/getting-started/server-and-client-components?utm_source=slothbytes.beehiiv.com&utm_medium=referral&utm_campaign=react-server-components-for-dummies)。
        
    - 在水合期间：
        
        - **函数组件**：执行函数体，但 `useEffect` 会在 DOM 完全构建完成后**异步执行**。
            
        - **类组件**：生命周期顺序是 `constructor` -> `getDerivedStateFromProps` -> `render` -> `componentDidMount`（在 `useEffect` 之后，但通常也在这阶段）。
            
2. **后续导航**
    
    - 当你在应用中通过 Link 组件跳转时，Next.js **不会**再次请求完整的 HTML。
        
    - 它会仅获取 RSC Payload，然后**只在客户端重新渲染** Client Components，此时 Server Components 不再参与 [](https://nextjscn.org/docs/app/getting-started/server-and-client-components#examples)[](https://nextjs.org/docs/app/getting-started/server-and-client-components?utm_source=slothbytes.beehiiv.com&utm_medium=referral&utm_campaign=react-server-components-for-dummies)。
        
    - 在后续导航中，生命周期会完全按照 React 的正常机制运行（例如 `props` 改变触发 `componentDidUpdate` 或 `useEffect` 重新执行）。


