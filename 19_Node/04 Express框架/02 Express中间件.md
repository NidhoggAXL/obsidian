# 一、认识中间件

xpress是一个路由和中间件的Web框架，它本身的功能非常少： Express应用程序本质上是一系列中间件函数的调用；

中间件是什么呢？
 - 中间件的本质是传递给express的一个回调函数；
 - 这个回调函数接受三个参数：
	 - 请求对象（request对象）；
	 - 响应对象（response对象）；
	 - next函数（在express中定义的用于执行下一个中间件的函数） - 

中间件中可以执行哪些任务呢？

 - 执行任何代码；
 - 更改请求（request）和响应（response）对象；
 - 结束请求-响应周期（返回数据）；
 - 调用栈中的下一个中间件；

如果当前中间件功能**没有结束请求-响应周期**，则**必须调用next()将控制权传递给下一个中间件功能**，否则，请求将被挂起。


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766214561000hzb00p.png)

# 二、自己编写中间件

那么，如何将一个中间件应用到我们的应用程序中呢？

- express主要提供了两种方式：
	 - app/router.use；
	 - app/router.methods；
 - 可以是 app，也可以是router，router我们后续再学习:
 - methods指的是常用的请求方式，比如： app.get或app.post等；

先来学习use的用法，因为methods的方式本质是use的特殊情况；

## 2.1 最普通的中间件

通过use方法注册的中间件**是最普通的/简单的中间件**

通过use注册的中间件，无论是什么请求方式都可以匹配上:

 - 无论是 GET 、POST、DELE等请求。
 - 无论什么请求路劲：`\home`、`\login`。

```js
import express from 'express'

// 创建开启服务器
const app = express()

// 第一个普通中间件
app.use((req, res, next) => {
  console.log("普通中间件——01")
  next()
})

// 第二个中间件
app.use((req, res, next) => {
  console.log("普通中间件——02")
  res.end("ok")// 结束请求
})

// 监听接口
app.listen(8000, () => {
  console.log("服务器开始成功")
})

// 服务器开始成功
// 普通中间件——01
// 普通中间件——02
```


> [!abstrat] 总结:
> 当express接收到客户端发送的网络请求时，在所有中间中开始进行匹配,当匹配到第一个符合要求的中间件时，那么就会执行这个中间件
> **后续的中间件是否会执行呢?.取决于上一个中间件有没有执行next**

## 2.2 path匹配中间件

path匹配中间件不会对请求方式（method）进行限制

```js
import express from 'express'

// 创建开启服务器
const app = express()

// path匹配间件
// 请求 URL ：http://localhost:8000/home
app.use("/home", (req, res, next) => {
  console.log("home 路径匹配中间件")
  res.end("OK")
})
// 监听接口
app.listen(8000, () => {
  console.log("服务器开始成功")
})

// 服务器开始成功
// home 路径匹配中间件

```

## 2.3 path和metho中间件

使用 `app.method(path, middleware)` 来使用

```js
import express from 'express'

// 创建开启服务器
const app = express()

// path和method匹配间件
// get 请求
app.get("/home", (req, res, next) => {
  res.send("get请求")
})
// post 请求
app.post("/home", (req, res, next) => {
  res.send("post请求")
})

// 监听接口
app.listen(8000, () => {
  console.log("服务器开始成功")
})

```

## 2.4 注册多个中间件

使用的语法：`app.get(path, middleware, middleware, middleware, ...)`

```js
import express from 'express'

// 创建开启服务器
const app = express()

// 注册多个中间件
app.use((req, res, next) => {
  console.log("中间件1")
  next()
}, (req, res, next) => {
  console.log("中间件2")
  next()
}, (req, res, next) => {
  console.log("中间件3")
  res.end("放回数据")
})

// 监听接口
app.listen(8000, () => {
  console.log("服务器开始成功")
})

// 服务器开始成功
// 中间件1
// 中间件2
// 中间件3
```

# 三、中间件body解析

并非所有的中间件都需要我们从零去编写：

 - express有内置一些帮助我们完成对request解析的中间件；
 - registry仓库中也有很多可以辅助我们开发的中间件；

在客户端发送post请求时，会将数据放到body中：

 - 客户端可以通过json的方式传递；
 - 也可以通过form表单的方式传递；

案例：进行登录和注册的监听

- 方式一：基础的编写
- 方式二：使用中间件
- 方式三：express 提供的中间件

## 3.1 基础编写

```js
import express from 'express'

const app = express()

// 监听登录
app.post("/login", (req, res, next) => {
  let isLogin = false
  req.on("data", (data) => {
    const dataString = data.toString()
    const dataInfo = JSON.parse(dataString)
    if (dataInfo.username === "admin" && dataInfo.password === "123456") {
      isLogin = true
    }
  })
  req.on("end", () => {
    if (isLogin) {
      res.end("登录成功")
    } else {
      res.end("登录失败, 请重新检查帐号和密码")
    }
  })
})

// 监听注册
app.post("/register", (req, res, next) => {
  let isRegister = false
  req.on("data", (data) => {
    const dataString = data.toString()
    const dataInfo = JSON.parse(dataString)
    // 到数据库查询是否注册过
    isRegister = true
  })
    req.on("end", () => {
    if (isRegister) {
      res.end("注册成功")
    } else {
      res.end("已经注册过，请登录")
    }
  })
})

app.listen(8000)
```

## 3.2 使用中间件

```js
import express from "express";

const app = express();

// 通用中间件
app.use((req, res, next) => {
  if (req.headers["content-type"] === "application/json") {
    req.on("data", (data) => {
      const dataInfo = JSON.parse(data.toString());
      req.body = dataInfo;
    });
    req.on("end", () => {
      next(); // 执行下一个中间件
    });
  } else {
    next(); // 执行下一个中间件
  }
});

// 登录中间件
app.post("/login", (req, res) => {
  if (req.body.username === "admin" && req.body.password === "123456") {
    res.end("登录成功");
  } else {
    res.end("登录失败, 帐号或者密码错误");
  }
});

// 注册中间件
app.post("/register", (req, res) => {
  // 数据库查询是否注册过
  if (req.body.username === "admin" && req.body.password === "123456") {
    res.end("已经存在帐号，请登录");
  } else {
    res.end("注册成功");
  }
});

app.listen(8000);

```

## 3.3 express的中间件

使用 express.json 的中间件：

```js
import express from "express";

const app = express();

// 通用中间件
// app.use((req, res, next) => {
//   if (req.headers["content-type"] === "application/json") {
//     req.on("data", (data) => {
//       const dataInfo = JSON.parse(data.toString());
//       req.body = dataInfo;
//     });
//     req.on("end", () => {
//       next(); // 执行下一个中间件
//     });
//   } else {
//     next(); // 执行下一个中间件
//   }
// });

// 直接使用 express 中间件,就是上面通用中间件的一个封装
app.use(express.json());

// 登录中间件
app.post("/login", (req, res) => {
  if (req.body.username === "admin" && req.body.password === "123456") {
    res.end("登录成功");
  } else {
    res.end("登录失败, 帐号或者密码错误");
  }
});

// 注册中间件
app.post("/register", (req, res) => {
  // 数据库查询是否注册过
  if (req.body.username === "admin" && req.body.password === "123456") {
    res.end("已经存在帐号，请登录");
  } else {
    res.end("注册成功");
  }
});

app.listen(8000);

```


# 四、express内置中间件

## 4.1 express.json

可以使用expres内置的中间件或者使用body-parser来完成：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766221125000vn0tjj.png)

## 4.2 express.urlencoded

如果解析的是 application/x-www-form-urlencoded：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766221161000x6s61e.png)

extended 的作用是什么呢？

| 选项                    | 解析库             | 功能特点             | 适用场景            |
| --------------------- | --------------- | ---------------- | --------------- |
| `{ extended: false }` | `querystring` 库 | 只支持简单键值对，不支持嵌套对象 | 简单表单数据          |
| `{ extended: true }`  | `qs` 库          | 支持嵌套对象、数组等复杂结构   | REST API、复杂数据结构 |
# 五、第三方中间件

## 5.1 请求日志-morgan

如果我们希望将请求日志记录下来，那么可以使用express官网开发的第三方库：**morgan**

> [!tip] 注意：需要单独安装 `npm install morgan`

```js
import express from 'express'
import morgan from 'morgan'
import fs from 'fs'

// 开启服务器
const app = express()

// 创建写入流
const writeStream = fs.createWriteStream("./logs/access.log")
// 使用morgan中间件
app.use(morgan("combined", { stream: writeStream }))

// 中间件
app.use((req, res, next) => {
  res.end("OK")
})

// 监听启动
app.listen(8000)

```

发送两次网络请求后，得到的文件里面写入的数据：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176622192300060zpl5.png)

## 5.2 文件上传-multer

可以使用express提供的multer来完成：

```bash
npm install multer
```

---

### 单文件上传

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766229896000u0iplv.png)

```js
import express from "express";
import multer from "multer";

// 开启服务器
const app = express();

// 创建multe
const upload = multer({ dest: "./uploads" });
//dest-desitination(目的地)

// 中间件
app.post("/upload", upload.single("phone"), (req, res, next) => {
  console.log(req.file); //获取到文件的信息
  res.end("文件上传成功~");
});

// 监听启动
app.listen(8000, () => {
  console.log("服务开启成功")
});

```

可以在控制台看到文件的信息：


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766229980000aduptl.png)

> [!tip]
> 在 Window 电脑上面，需要为文件添加后缀名才可以正确的显示图片，不然电脑识别不了。
> 
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766230054000406it1.png)

### 添加后缀名

```js
import express from "express";
import multer from "multer";

// 开启服务器
const app = express();

const upload = multer({
  // diskStorage-磁盘存储
  storage: multer.diskStorage({
    // 文件存储路径
    destination: (req, file, callback) => {
      callback(null, "./uploads");
    },
    // 文件重命名
    filename: (req, file, callback) => {
      // 时间戳 + 原始文件名(存在后缀)
      callback(null, Date.now() + "_" + file.originalname);
    },
  }),
});

// 中间件
// pload.single("phone") 为 form-data 里面的key
app.post("/upload", upload.single("phone"), (req, res, next) => {
  console.log(req.file)
  res.end("OK");
});

// 监听启动
app.listen(8000);

```

### 多文件上传

在 PostMan 中一次选择多张图片：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766232101000n8xkve.png)

> [!note] 第一个 phones 里面 2 files 就是我在一个 kye=value 中选择了两个文件

只需要把前面的上传的方法切换为 arrary 就可以啦：

```js
// pload.single("phone") 为 form-data 里面的key
app.post("/upload", upload.array("phones"), (req, res, next) => {
  console.log(req.files)// 获取到的文件信息，存储在数组中
  res.end("多文件上传成功------");
});
```

### 解析form-data

如果我们希望借助于multer帮助我们解析一些form-data中的普通数据，那么我们可以使用 any：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766233121000hkpph5.png)


```js
import express from 'express'
import multer from 'multer'

// 开启服务器
const app = express()

const formdta = multer()

// 中间件
//formdta.any()解析所有文件
app.post("/upload", formdta.any() , (req, res, next) => {
  console.log(req.body)
  //[Object: null prototype] { username: 'axl', password: '123' }
  res.end("文件上传成功")
})

// 监听启动
app.listen(8000)

```


