
# 一、params

请求地址：http://localhost:8000/users/123

获取params：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766307536000o2vhfh.png)

# 二、query

请求地址：http://localhost:8000/login?username=why&password=123

获取query：


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766307569000ppeos3.png)

# 三、json

请求地址：http://localhost:8000/login

body是json格式：

```json
{
  "username": "axl",
  "password": "123"
}
```

获取json数据：

 - 安装依赖： `npm install koa-bodyparser`
 - 使用 koa-bodyparser 的中间件；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766307649000xkw1ce.png)

# 四、x-www-form-urlencoded

请求地址：http://localhost:8000/login

body是x-www-form-urlencoded格式：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766307726000gtxxqu.png)

获取json数据：(和json是一致的)

 - 安装依赖： `npm install koa-bodyparser`
 - 使用 koa-bodyparser的中间件；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766307756000k3wgyz.png)

# 五、form-data

请求地址：http://localhost:8000/login

body是form-data格式

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176630780600022znof.png)

解析body中的数据，我们需要使用multer

 - 安装依赖：`npm install koa-multer multer`
 - 使用 multer中间件；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17663078370005bm5du.png)


