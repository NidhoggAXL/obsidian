
在后台管理系统中，登录后的基本所有请求都是要携带 token 发送网络请求的，那么 token 需要如何携带？是不是每次发送网络请求都要手动携带 token ？

**token 携带**：token 放入到请求头 headers 的 Authorization(授权) 中，并且 token 需要在前面凭借一个特殊的字符串，一般是 Bearer(持证人) 。

```ts
//  URL
axios.get({
  url: "/login",
  // token保存到henders的Authorization(授权)中
  headers: {
    Authorization: "Bearer" + 携带token
  }
})
```

token携带的封装：首先就是对网络请求 [[01 TS封装axios|TS封装axios]] ，然后在其创建实例的时候添加 [[07 路由导航守卫钩子|路由守卫钩子]] ，当发送网络请求成功的时候，进行一个拦截，对拦截的的配置中添加 headers 的配置。

```ts
import MYAxios from "./request"

const xlRequest = new MYAxios({
  baseURL: BASE_URL,
  timeout: TIME_OUT,
  //在创建实例的时候，添加路由守卫钩子
  //对 config 进行配置，并返回
  //以返回的配置，真正发送网络请求
  interceptors: {
    requestSucess: (config) => {
      const token = localCache.getItem(TOKEN)
      //需要进行类型缩小，因为headers是可选的，且token不一定有值
      if (config.headers && token)//类型缩小
        config.headers.Authorization = "Bearer" + 携带token
      return config
    }
  }
})
```




