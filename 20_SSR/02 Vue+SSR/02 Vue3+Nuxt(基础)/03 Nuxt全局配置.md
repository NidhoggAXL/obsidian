# 一、Nuxt配置

nuxt.config.ts 配置文件位于项目的根目录，可对Nuxt进行自定义配置。比如，可以进行如下配置：

# 二、runtimeConfig

runtimeConfig：运行时配置，即定义环境变量

- 可通过.env文件中的环境变量来覆盖，优先级（**.env > runtimeConfig**）
- **`.env`的变量会打入到process.env中**，符合规则的会覆盖runtimeConfig的变量
- `.env`一般用于某些终端启动应用时动态指定配置，同时支持dev和pro

```ts
// nuxt.config.js
// https://nuxt.com/docs/api/configuration/nuxt-config
export default defineNuxtConfig({
  /** * 兼容性日期配置 * 指定了项目的兼容性日期为2025年7月15日 * 这可能用于确保API和功能与特定版本的兼容性 */
  compatibilityDate: '2025-07-15', 
  /** * 开发工具配置 * enabled: true 表示启用开发工具 * 开发工具可能提供调试、性能分析等功能，有助于开发过程中的问题排查和优化 */
  devtools: { enabled: true }, 

  runtimeConfig: {
    appKey: "aabbcc",//server
    public: {
      baseURL: "http://axl_nuxt.com"// srever and client
    }
  }
})

```

```shell title=".env"
NUXT_APP_KEY = "AXL"
NUXT_PUBLIC_BASE_URL = "localhost"
NUXT_WHY = 'why'
```


```vue
// app.vue
<template>
  <div>
    <h2>Hello Nuxt</h2>
  </div>
</template>

<script setup>
// 获取nuxt.config.js中配置的变量
const runtimeConfig = useRuntimeConfig();
if (process.server) {
  console.log("运行在 server");
  console.log(runtimeConfig.appKey, runtimeConfig.public.baseURL);
}
if (process.client) {
  console.log("运行在 client");
  // client环境获取不到 appkey
  console.log(runtimeConfig.appKey, runtimeConfig.public.baseURL);
}
</script>

```

# 三、appConfig

appConfig： 应用配置，定义在**构建时确定的公共变量**，如：theme

  - 配置会和 app.config.ts 的配置合并（**优先级 app.config.ts > appConfig**）

```vue
// ./app/app.vue
<template>
  <div>
    <h2>Hello Nuxt</h2>
  </div>
</template>

<script setup>
// 打印appConfig的配置
console.log(useAppConfig().title)
console.log(useAppConfig().them.primary)

</script>

```

```ts
// ./app/app.config.ts
export default defineAppConfig({
  title: '这个是覆盖nuxt.config.ts的配置',
})
```

```ts
// ./nuxt.config.ts
export default defineNuxtConfig({
  // 定义app的配置(server and client)
  appConfig: {
    title: "hello nuxt",
    them: {
      primary: "red"
    }
  }
})

```

# 四、app

app：app配置 

- head：给每个页面上设置head信息，也支持 useHead 配置和内置组件。
- 不仅可以添加head里面的标签，body里面的标签也可以
- 优先级：内置组件 > useHead > nuxt.config.js里面的app配置

```js
// nuxt.config.js
export default defineNuxtConfig({
  // 定义app的head配置
  app: {
    head: {
      title: "hello nuxt",
      meta: [
        { name: "description", content: "hello nuxt" }
      ]
    }
  }
})

```


```vue
// app.vue
<template>
  <div>
    <h2>Hello Nuxt</h2>
    <Head>
      <Link rel="icon" href="/favicon.ico" />
      <Script src="https://unpkg.com/element-plus/lib/index.full.js"></Script>
      <Body>
        <div id="aaaaaaa"></div>
      </Body>
    </Head>
  </div>
</template>

<script setup>

useHead({
  title: "Hello Nuxt",
  meta: [
    { name: "description", content: "My amazing site." },
    { name: "keywords", content: "nuxt, vue, javascript" },
  ],
})

</script>

```

# 五、ssr

ssr：指定应用渲染模式

```js
// next.config.js
// https://nuxt.com/docs/api/configuration/nuxt-config
export default defineNuxtConfig({
  // 指定渲染模式
  // false就是一个spa的渲染模式
  ssr: false,
});

```

# 六、router

router：配置路由相关的信息，比如在客户端渲染可以配置hash路由

```js
// next.config.js
// https://nuxt.com/docs/api/configuration/nuxt-config
export default defineNuxtConfig({
  // 指定渲染模式
  // false就是一个spa的渲染模式
  ssr: false,
  router: {
    options: {
      // 开启hash路由，只有在spa渲染模式生效
      hashMode: true
    }
  }
});

```


# 七、其他配置

alias：路径的别名，默认已配好

 modules：配置Nuxt扩展的模块，比如：@pinia/nuxt @nuxt/image

 routeRules：定义路由规则，可更改路由的渲染模式或分配基于路由缓存策略（公测阶段）

builder：可指定用 vite 还是 webpack来构建应用，默认是vite。如切换为 webpack 还需要安装额外的依赖。

# 八、应用配置（app.config）

Nuxt 3 提供了一个 app.config.ts 应用配置文件，用来定义在**构建时确定的公共变量**，例如：

 - 网站的标题、主题色 以及任何不敏感的项目配置

app.config.ts 配置文件中的选项不能使用env环境变量来覆盖，与 runtimeConfig 不同

不要将**秘密或敏感信息**放在 app.config.ts 文件中，该文件是客户端公开

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773902608000ugiuju.png)

# 九、runtimeConifg vs app.config

runtimeConfig 和 app.config都用于向应用程序公开变量。要确定是否应该使用其中一种，以下是一些指导原则：

 - runtimeConfig：定义环境变量，比如：运行时需要指定的私有或公共token。
 - app.config：定义公共变量，比如：在构建时确定的公共token、网站配置。


