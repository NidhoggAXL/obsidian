# 一、认识useId

官方的解释:useld 是一个用于生成横跨服务端和客户端的稳定的唯- ID 的同时避免 hydration 不匹配的 hook。

这里有一个词叫hydration，要想理解这个词，我们需要理解一些服务器端渲染(SSR)的概念。

**什么是SSR?**

- SSR(Server Side Rendering，服务端渲染)指的是页面在服务器端已经生成了完成的HTML页面结构，**不需要浏览通过执行JS代码，创建页面结构;**
- 对应的是CSR(Client Side Rendering，客户端渲染)我们开发的 SPA页面 通常依赖的就是客户端渲染;

早期的服务端渲染包括PHP、JSP、ASP等方式，但是在目前前后端分离的开发模式下，前端开发人员不太可能再去学习PHP、JSP等技术来开发网页;

不过我们可以**借助于Node来帮助我们执行JavaScript代码，提前完成页面的渲染**;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755847155000jwoe2x.png)

# 二、SSR同构应用

什么是同构应用？  **一套代码既可以在服务端运行又可以在客户端运行**，这就是同构应用。 

同构是一种SSR的形态，是现代SSR的一种表现形式。 

- 当用户发出请求时，先在服务器通过SSR渲染出首页的内容。
- 但是对应的代码同样可以在客户端被执行。 
- **执行的目的包括事件绑定等以及其他页面切换时也可以在客户端被渲染**；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755847185000kgn5m3.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755847192000zc2lgg.png)

# 三、Hydration

什么是Hydration？这里我引入vite-plugin-ssr插件的官方解释。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175584720600063whoq.png)

在进行 SSR 时，我们的页面会呈现为 HTML。 

- 但仅 HTML 不足以使页面具有交互性。例如，浏览器端 JavaScript 为零的页面不能是交互式的（没有 JavaScript 事件处理程序来响应用 户操作，例如单击按钮）。 
- 为了使我们的页面具有交互性，除了在 Node.js 中将页面呈现为 HTML 之外，我们的 UI 框架（Vue/React/...）还在浏览器中加载和呈现 页面。（它创建页面的内部表示，然后将内部表示映射到我们在 Node.js 中呈现的 HTML 的 DOM 元素。）

> [!node] 这个过程称为hydration。

# 四、useId的作用

再来看一遍：useId 是一个用于生成横跨服务端和客户端的稳定的唯一 ID 的同时避免 hydration 不匹配的 hook。 

所以我们可以得出如下结论：

- useId是用于react的同构应用开发的，前端的SPA页面并不需要使用它； 
- useId可以保证应用程序在客户端和服务器端生成唯一的ID，这样可以有效的避免通过一些手段生成的id不一致，造成 hydration mismatch；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17558472930008fcxn4.png)


