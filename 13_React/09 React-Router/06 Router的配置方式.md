# Router版本5与6的区别

前面所有的路由定义都是直接使用Route组件，并且添加属性来完成的。 

但是这样的方式会让路由变得非常混乱，我们希望将所有的路由配置放到一个地方进行集中管理： 

- 在早期的时候，Router并且没有提供相关的API，我们需要借助于react-router-config完成；
- 在Router6.x中，为我们提供了useRoutes API可以完成相关的配置；

先来看一个表格，快速了解 React Router 中路由配置的几种主要方式及其特点：


| **特性** |       **Routes/Route 组件**       |            **useRoutes Hook (推荐)**             |      **备注 (主要针对 v6 及以上)**      |
| :----: | :-----------------------------: | :--------------------------------------------: | :----------------------------: |
|  **配置形式**  |            JSX 标签形式             |                     对象数组形式                     | useRoutes 的配置更集中，类似 Vue Router |
|  **嵌套路由**  |       <Route> 嵌套或 Outlet        |                 通过 children 属性                 | 父路由元素中需放置 <Outlet /> 组件来渲染子路由  |
| **路径匹配规则** | 默认精确匹配，如需匹配子路由，则在父路由 path 后加 /* |                     同组件形式                      |       V6 版本移除了 exact 属性        |
| **路由重定向**  |        使用 <Navigate> 组件         | 在配置数组中可使用 {redirect: true, to: "/path"} 等自定义字段 |        通常结合路由拦截或统一配置使用         |
| **路由懒加载**  |  需配合 React.lazy 和 Suspense 使用   |                  同上，可在配置数组中实现                  |           提升应用初始加载性能           |
|  **路由拦截**  |          需自定义包装组件或高阶组件          |       易于在统一路由管理中实现全局前置守卫 (onRouteBefore)       |        常用于权限控制、登录状态检查等         |
|  **类型支持**  |               良好                |                       良好                       |       对 TypeScript 支持友好        |

# 🌐 首先配置路由环境

在开始之前，你需要确保已经安装了 react-router

```bash
npm install react-router
```

接着，通常需要在应用顶层用 `<BrowserRouter>`（推荐）或 `<HashRouter>` 包裹你的应用组件，以确保路由上下文可用：

```jsx
// index.js 或 main.jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import App from './App.jsx'
import { BrowserRouter } from 'react-router'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    {/* 使用 BrowserRouter 包裹 App */}
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </StrictMode>,
)
```

# 🛣️ 配置路由的两种方式

React Router v6 及以后版本主要推荐以下两种配置路由的方式：

- **使用 `<Routes>` 和 `<Route>` 组件 (JSX 形式)**：这种方式直接在组件的 JSX 中定义路由结构，直观明了。
- **使用 useRoutes Hook (对象数组形式)**：这种方式通过一个 JavaScript 对象数组来定义路由，更加灵活和推荐，尤其对于复杂的路由结构或需要统一管理路由的场景。

## 1. 使用 `<Routes>` 和 `<Route>` 组件

这是在组件内部直接书写 JSX 来定义路由的方式。

```jsx
// App.jsx
import { Routes, Route } from 'react-router-dom';
import Home from './pages/Home';
import About from './pages/About';
import User from './pages/User';
import NotFound from './pages/NotFound';

function App() {
  return (
    <div>
      {/* 定义路由映射关系 */}
      <Routes>
        {/* path 定义路径，element 指定要渲染的组件 */}
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/user/:userId" element={<User />} /> {/* 动态路由 */}
        <Route path="*" element={<NotFound />} /> {/* 404 页面 */}
      </Routes>
    </div>
  );
}

export default App;
```

## 2. 使用 useRoutes Hook (推荐)

useRoutes 允许你使用一个 JavaScript 对象数组来定义路由，这使得路由配置更加集中和灵活，特别是在处理嵌套路由和复杂逻辑时。

```jsx
// App.jsx
import { useRoutes } from 'react-router-dom';
import Home from './pages/Home';
import About from './pages/About';
import User from './pages/User';
import NotFound from './pages/NotFound';

// 1. 定义路由配置数组
const routes = [
  {
    path: '/',
    element: <Home />,
  },
  {
    path: '/about',
    element: <About />,
  },
  {
    path: '/user/:userId', // 动态路由参数
    element: <User />,
  },
  {
    path: '*', // 匹配所有未定义的路由
    element: <NotFound />,
  },
];

function App() {
  // 2. 使用 useRoutes Hook 根据配置生成路由结构
  const routing = useRoutes(routes);

  return <div>{routing}</div>;
}

export default App;
```

# 🧩 处理嵌套路由

嵌套路由是指路由之间存在父子关系，子路由的路径是基于父路由路径的。

- 父路由组件：需要在父组件的希望子组件渲染的位置放置 `<Outlet />` 组件。
- 路由配置：
    - 在 JSX 形式中，使用嵌套的 `<Route>` 标签。
    - 在 useRoutes 形式中，使用 children 属性。

例如，假设有 `/products` 和它的子路由 `/products/list`, `/products/:id`：

```jsx
// 使用 useRoutes 配置嵌套路由
const routes = [
  // ... 其他路由
  {
    path: '/products',
    element: <ProductLayout />, // 父组件，内部需要包含 <Outlet />
    children: [ // 子路由配置
      {
        path: 'list', // 注意这里不是 '/list'
        element: <ProductList />,
      },
      {
        path: ':id', // 匹配 /products/123
        element: <ProductDetail />,
      },
      // 可以设置一个默认子路由，当访问 /products 时渲染
      {
        index: true, // 或者 path: ''
        element: <ProductDefaultPage />,
      },
    ],
  },
];
```

```jsx
// ProductLayout.jsx
import { Outlet, Link } from 'react-router-dom';

function ProductLayout() {
  return (
    <div>
      <h2>产品中心</h2>
      <nav>
        <Link to="list">产品列表</Link> {/* 注意这里的链接是相对路径 */}
      </nav>
      {/* Outlet 是子组件渲染的位置 */}
      <Outlet />
    </div>
  );
}
```


# 🧭 路由跳转与重定向

## 1. 路由跳转

进行页面导航（跳转）主要有两种方式：

- 声明式导航：使用 `<Link>` 或 `<NavLink>` (可提供激活状态样式) 组件。

```jsx
import { Link, NavLink } from 'react-router-dom';

function Navigation() {
  return (
    <nav>
      <Link to="/">首页</Link>
      <NavLink to="/about" style={({ isActive }) => ({ color: isActive ? 'red' : 'blue' })}>
        关于
      </NavLink>
    </nav>
  );
}
```

- 编程式导航：在函数组件中，使用 useNavigate Hook。

```jsx
import { useNavigate } from 'react-router-dom';

function HomePage() {
  const navigate = useNavigate();

  const handleClick = () => {
    navigate('/about'); // 跳转到 /about
    // navigate(-1); // 后退一页
    // navigate('/user/123', { replace: true }); // 替换当前历史记录
  };

  return (
    <button onClick={handleClick}>前往关于页面</button>
  );
}
```

**对于类组件**，React Router v6 及以上版本不再提供 withRouter 高阶组件。你需要自己创建一个 [[04 Router的代码跳转|HOC ]]来注入 navigate 函数，或者更**推荐的方式是将类组件转换为函数组件**。

## 2. 路由重定向

可以使用 `<Navigate>` 组件来实现重定向：

```jsx
import { Navigate } from 'react-router-dom';

// 在路由配置中，将根路径 / 重定向到 /home
{
  path: '/',
  element: <Navigate to="/home" replace />,
}
```

**你也可以在组件渲染过程中根据条件返回  `<Navigate>` 组件来实现动态重定向。**

# ⚡ 路由懒加载

对于大型应用，为了优化首屏加载速度，可以使用 React.lazy 和 [[03 Vue内置组件Suspense|Suspense]] 来实现路由组件的懒加载（按需加载）：

```jsx
import React, { Suspense } from 'react';
import { useRoutes } from 'react-router-dom';

// 使用 React.lazy 动态导入组件
const Home = React.lazy(() => import('./pages/Home'));
const About = React.lazy(() => import('./pages/About'));
// ... 其他懒加载组件

const routes = [
  { path: '/', element: <Home /> },
  { path: '/about', element: <About /> },
  // ...
];

function App() {
  const routing = useRoutes(routes);

  return (
    // 使用 Suspense 包裹，fallback 属性指定加载中的提示
    <Suspense fallback={<div>Loading...</div>}>
      {routing}
    </Suspense>
  );
}

export default App;
```

# 🛡️ 路由拦截与权限控制

你可以在路由渲染之前或之后加入自定义逻辑，例如检查用户登录状态。一种常见的模式是创建一个**路由守卫组件**或在**统一路由配置中实现拦截逻辑**：

```jsx
// 一个简单的高阶组件示例 (概念性)
import { useNavigate, useLocation } from 'react-router-dom';

function withAuth(Component) {
  return function AuthenticatedComponent(props) {
    const isLoggedIn = !!localStorage.getItem('authToken'); // 假设用 token 判断
    const navigate = useNavigate();
    const location = useLocation();

    if (!isLoggedIn) {
      // 未登录则重定向到登录页，并记录从哪里跳转的
      navigate('/login', { replace: true, state: { from: location } });
      return null;
    }

    return <Component {...props} />;
  };
}

// 在路由配置中使用
{
  path: '/dashboard',
  element: withAuth(<Dashboard />),
}
```

更复杂和集中的路由拦截通常会在 useRoutes 的配置数组和自定义的转换逻辑中实现。


