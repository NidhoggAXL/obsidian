
**传递参数有二种方式：** 

- 动态路由的方式； 
- search传递参数； 

**[[04 动态路由和路由嵌套|动态路由]]的概念指的是路由中的路径并不会固定：** 

- 比如/detail的path对应一个组件Detail； 
- 如果我们将path在Route匹配时写成`/detail/:id`，那么 /detail/abc、/detail/123都可以匹配到该Route，并且进行显示； 
- 这个匹配规则，我们就称之为动态路由； 
- 通常情况下，使用动态路由可以为路由传递参数。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17556949400005xdtte.png)

**search传递参数**：[[04 ES10#二、Object fromEntries|Object fromEntries]]

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755695119000nad6l6.png)




