
koa并没有内置部署相关的功能，所以我们需要使用第三方库：

```bash
npm install koa-static
```

部署的过程类似于[Express](05%20Express静态服务器.md)：

```js
import koa from "koa";
import KoaRouter from '@koa/router'
import KoaStatic from 'koa-static'

// 创建服务器
const app = new koa();

// 静态资源部署
app.use(KoaStatic("./dist"))


// 监听接口
app.listen(3000, () => {
  console.log("服务器启动成功");
});

```



