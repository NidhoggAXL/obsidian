**传递参数有二种方式：** 

- 动态路由的方式； 
- search传递参数； 

**[动态路由](10_Vue3/13%20Vue-Router/04%20动态路由和路由嵌套.md)的概念指的是路由中的路径并不会固定：** 

- 比如 `/detail` 的path对应一个组件Detail； 
- 如果将path在Route匹配时写成`/detail/:id`，那么 `/detail/abc`、`/detail/123` 都可以匹配到该Route，并且进行显示； 
- 这个匹配规则，我们就称之为动态路由； 
- 通常情况下，使用动态路由可以为路由传递参数。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17556949400005xdtte.png)

**search传递参数**：[](07_JavaScript高级/10%20ES6~ES13特性/04%20ES10.md#二、Object%20fromEntries|Object.fromEntries)

```jsx
// 定义Link跳转
<Link to = "suser?name=axl&age=19">用户信息</Link>

//获取参数
const [searchParams] = useSearchParpams()
//将获取的数组装换为对象
const query = Object.fromEntries(searchParms)
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755695119000nad6l6.png)




