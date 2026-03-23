Nuxt3支持自定义插件进行扩展，创建插件有两种方式：

方式一：直接使用 useNuxtApp() 中的 provide(name, vlaue) 方法直接创建，比如：可在App.vue中创建

 - useNuxtApp 提供了访问 Nuxt 共享**运行时上下文**的方法和属性（**两端可用**）：provide、hooks、callhook、vueApp等

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774074412000bul1s6.png)

方式二：在 plugins 目录中创建插件（**推荐**）

 - 顶级和子目录index文件写的插件会在创建Vue应用程序时会自动加载和注册
 - .server 或 .client 后缀名插件，可区分服务器端或客户端，**用时需区分环境**

在 plugins 目录中创建插件

 - 1.在 plugins 目录下创建 plugins/price.ts 插件
 - 2.接着 defineNuxtPlugin 函数创建插件，参数是一个回调函数
 - 3.然后在组件中使用 useNuxtApp() 来拿到插件中的方法


```js
// app/plugins/formatePrice.client.ts
export default defineNuxtPlugin(() => ({
  provide: {
    formatePrice: (price: string) => {
      return price + "￥"
    }
  }
}))
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17740747350005h2ae9.png)

> [!tip] 注意事项：
> 插件注册顺序可以通过在文件名前加上一个**数字来控制插件注册的顺序**
> 比如：plugins/1.price.ts 、plugins/2.string.ts、plugins/3.date.ts
> 


 