# 一、错误处理方案

服务器端的错误处理 方案有下面两种方案：

方案一：放回http错误码（基础使用）

```js
res.status(401)
res.json("未授权访问的信息")
```
 方案二：http 正常返回(状态码:200)，在返回信息中包含错误

```js
res.json({
  coder: -1001,
  message: "未授权访问的信息，请检查token"
})
```

> [!tip]
> 第一种可以定义的错误信息较少，但是简单
> 第二种可以自定义错误码和信息，需要建立接口信息文档，比较浪费时间

# 二、案例

用户登录的案例：

 - 错误码：-1001，没有输入用户名和密码
 - 错误码：-1002，输入用户名和密码
 - 未知错误

```js
import express from "express";
import { token } from "morgan";

// 开启服务器
const app = express();

// json编码
app.use(express.json());

app.post("/login", (req, res, next) => {
  // 判断re1q.body不为undefine和空对象
  if (req.body && Object.keys(req.body).length > 0) {
    const { username, password } = req.body;
    if (!username || !password) {
      next(-1001);
    } else if (username !== "admin" || password !== "123456") {
      next(-1002);
    } else {
      res.json({
        code: 200,
        message: "登录成功",
        token: "fldjlajsd",
      });
    }
  }
  next(-1001)
});

// 这里总共有四个参数
app.use((errCode, req, res, next) => {
  let code = errCode
  let message = "未知错误！！！"
  switch (code) {
    case -1001:
      message = "没有输入用户名或者密码"
      break
    case -1002:
      message = "用户名或密码错误"
      break
  }
  res.json({
    code,
    message
  })
})

app.listen(8000);

```
