# 一、基本封装

axios 使用类封装：

```ts
import axios from 'axios' //  引入axios库
//  从axios中导入AxiosInstance和AxiosRequestConfig类型
import { AxiosInstance, AxiosRequestConfig } from "axios";


class XLRequest {
  //  实例变量，用于存储 Axios 实例 AxiosInstance 是 Axios 库中定义的类型，表示一个 Axios 实例的接口
  instance: AxiosInstance;

  //rquest实例 => axios实例
  constructor(config: AxiosRequestConfig) {
    //  使用传入的配置创建axios实例并保存到当前实例的instance属性中
    this.instance = axios.create(config);
  }

  //封装网络请求的方法
  request(config: AxiosRequestConfig) {
    return this.instance.request(config); //  使用axios实例发起请求并返回结果
  }
}

export default XLRequest
```

定义基础变量：

```ts
export const BASE_URL = "http://codercba.com:1888/airbnb/api";
export const TIME_OUT = 10000
```

使用类和基础变量创建实例：

```ts
import { BASE_URL, TIME_OUT } from './config'
import XLRequset from './request/index'

export const xlRequest = new XLRequset({
  baseURL: BASE_URL,
  timeout: TIME_OUT
})
```

使用实例发送网络请求：

```ts
xlRequest.request({
  url: "/home/discount",
})
.then((res) => {
  console.log(res.data);
});
```

# 二、添加拦截器

## 2.1 全局拦截器

只要是通过 XLRquest 类创建的实例发送网络请求都会进行拦截：

```ts
import axios from 'axios' //  引入axios库
//  从axios中导入AxiosInstance和AxiosRequestConfig类型
import { AxiosInstance, AxiosRequestConfig } from "axios";


class XLRequest {
  //  实例变量，用于存储 Axios 实例 AxiosInstance 是 Axios 库中定义的类型，表示一个 Axios 实例的接口
  instance: AxiosInstance;

  //rquest实例 => axios实例
  constructor(config: AxiosRequestConfig) {
    //  使用传入的配置创建axios实例并保存到当前实例的instance属性中
    this.instance = axios.create(config);

    //全局拦截器
    //  请求拦截器
    this.instance.interceptors.request.use(config => {
      //  在请求发送之前执行一些操作，例如添加请求头等
      console.log("全局请求成功拦截")
      return config;
    }, err => {
      //  在请求发送失败时执行一些操作
      console.log("全局请求失败拦截")
      return err;
    })
    //  响应拦截器
    this.instance.interceptors.response.use(res => {
      //  在响应成功时执行一些操作
      console.log("全局响应成功拦截")
      return res;
    }, err => {
      console.log("全局响应失败拦截")
      return err;
    })
  }

  //封装网络请求的方法
  request(config: AxiosRequestConfig) {
    return this.instance.request(config); //  使用axios实例发起请求并返回结果
  }
}

export default XLRequest
```

## 2.2 精选拦截器



