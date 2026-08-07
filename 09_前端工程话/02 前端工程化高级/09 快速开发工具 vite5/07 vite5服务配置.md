# server as open

 端口与自动打开（`server.port` / `server.open`）

```js
export default defineConfig({
  server: {
    port: 8080,     // 使用 8080 端口（默认 5173）
    open: true      // 启动后自动打开浏览器
  }
})
```

若 `8080` 被占用，Vite 会自动尝试 `8081`。

# host

允许局域网访问（server.host）

```js
export default defineConfig({
  server: {
    host: '0.0.0.0'   // 或 true，让手机等设备能访问
  }
})
```

启动后控制台会显示 http://192.168.x.x:8080/。

# proxy

代理解决跨域（`server.proxy`）

为什么需要代理？

前端开发服务器（如 `http://localhost:8080`）在请求后端接口时，如果后端运行在不同端口（如 `http://localhost:3000`）或不同域名，浏览器会拦截[[01 跨域问题|跨域]]请求。代理将前端请求“转发”到后端，让浏览器误以为请求的是同一个源，从而绕过跨域限制。

## 最简代理配置

```js
export default defineConfig({
  server: {
    proxy: {
      '/api': 'http://localhost:3000'
    }
  }
})
```

**际效果**：  

当前端代码中发起 `fetch('/api/users')` 时，浏览器实际访问的地址是 `http://localhost:8080/api/users`（同源）。Vite 收到这个请求后，把它原样转发到 `http://localhost:3000/api/users`，再将后端返回的数据交给前端。

> [!tip] **注意**：
> 这里路径前缀 `/api` 会原样保留，所以后端必须存在 `/api/users` 路由。


## 进阶代理配置（带路径重写、跨域头修改）

```js
export default defineConfig({
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:3000',
        changeOrigin: true,                     // 重要：修改请求头中的 Origin
        rewrite: (path) => path.replace(/^\/api/, ''), // 去掉 /api 前缀
        secure: false,                          // 后端用 HTTPS 自签名证书时可忽略验证
        proxyTimeout: 5000,                     // 5 秒超时
        headers: {
          'X-Custom-Header': 'my-value'        // 额外添加请求头
        }
      }
    }
  }
})
```


各属性的实际效果详细举例:

- **`target`**：目标服务器地址。  
    例如 `target: 'http://localhost:3000'`，所有匹配 `/api` 的请求都会转发到这个地址。
    
- **`changeOrigin: true`**：修改请求头中的 `Origin` 字段为目标地址的域名。  
    如果不开启，后端收到的 `Origin` 可能是 `http://localhost:8080`，若后端校验 `Origin` 会拒绝。开启后，`Origin` 变为 `http://localhost:3000`，从而通过校验。
    
- **`rewrite` 路径重写**：  
    假设前端发起 `fetch('/api/users')`，
    
    - 没有 `rewrite` 时，转发到 `http://localhost:3000/api/users`。
        
    - 使用 `rewrite: (path) => path.replace(/^\/api/, '')` 后，路径中的 `/api` 被替换为空，最终转发到 `http://localhost:3000/users`。
        
    
> [!note] 
> 这通常用于后端接口没有 `/api` 前缀的情况，方便统一管理。
    
- **`secure: false`**：如果 `target` 是 HTTPS（如 `https://api.example.com`）且证书是自签名的，设为 `false` 可避免 `UNABLE_TO_VERIFY_LEAF_SIGNATURE` 错误。
    
- **`proxyTimeout`**：设置代理请求的超时时间（毫秒），超过后代理会主动中断请求。
    
- **`headers`**：为转发的请求添加自定义头，例如传递认证令牌

## 综合效果示例

假设前端代码：

```js
fetch('/api/users')
  .then(res => res.json())
  .then(data => console.log(data))
```

代理配置如上（带 `rewrite` 和 `changeOrigin`），实际发生的网络过程：

1. 浏览器请求 `http://localhost:8080/api/users`（同源，无跨域）。
    
2. Vite 接收到该请求，匹配到 `/api` 规则。
    
3. Vite 将路径中的 `/api` 删除，变为 `/users`。
    
4. Vite 向 `http://localhost:3000/users` 发起真实请求，并在请求头中加入 `Origin: http://localhost:3000`（因为 `changeOrigin: true`）。
    
5. 后端响应数据，Vite 原样返回给浏览器。
    

浏览器看到的请求地址始终是 `http://localhost:8080/api/users`，但实际数据来自 `http://localhost:3000/users`。


