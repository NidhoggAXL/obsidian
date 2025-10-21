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
  console.log(res);
});
```

# 二、添加拦截器

## 2.1 类拦截器

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

## 2.2 实例拦截器

对其他请求，添加精确的拦截器：类似于爱彼迎的数据请求

```ts
import axios from 'axios' //  引入axios库
//  从axios中导入AxiosInstance和AxiosRequestConfig类型
import {
  AxiosInstance,
  AxiosRequestConfig,
  AxiosResponse,
  InternalAxiosRequestConfig,
} from "axios";

// 自定义接口
interface XLInterceptors {
  // 请求成功拦截
  requestSuccessFn?: (
    config: InternalAxiosRequestConfig
  ) => InternalAxiosRequestConfig;
  // 请求失败拦截
  requestFailureFn?: (err: any) => any;
  // 响应成功拦截
  responseSuccessFn?: (res: AxiosResponse) => AxiosResponse;
  // 响应失败拦截
  responseFailureFn?: (err: any) => any;
}
//定义继承 AxisoRequestConfig 的接口
interface XLRequestConfig extends AxiosRequestConfig {
  interceptors?: XLInterceptors;
}


class XLRequest {
  //  实例变量，用于存储 Axios 实例 AxiosInstance 是 Axios 库中定义的类型，表示一个 Axios 实例的接口
  instance: AxiosInstance;

  //rquest实例 => axios实例
  constructor(config: XLRequestConfig) {
    //  使用传入的配置创建axios实例并保存到当前实例的instance属性中
    this.instance = axios.create(config);

    //全局拦截器
    //  请求拦截器
    this.instance.interceptors.request.use(
      (config) => {
        //  在请求发送之前执行一些操作，例如添加请求头等
        console.log("全局请求成功拦截");
        return config;
      },
      (err) => {
        //  在请求发送失败时执行一些操作
        console.log("全局请求失败拦截");
        return err;
      }
    );
    //  响应拦截器
    this.instance.interceptors.response.use(
      (res) => {
        //  在响应成功时执行一些操作
        console.log("全局响应成功拦截");
        return res;
      },
      (err) => {
        console.log("全局响应失败拦截");
        return err;
      }
    );

    //  如果传入的配置中包含拦截器，则添加到实例中(对爱彼迎特定添加拦截器)
    //  可以添加多个拦截器，拦截器不会覆盖，而是按顺序执行
    this.instance.interceptors.request.use(
      config.interceptors?.requestSuccessFn,
      config.interceptors?.requestFailureFn
    );
    this.instance.interceptors.response.use(
      config.interceptors?.responseSuccessFn,
      config.interceptors?.responseFailureFn
    )

  }

  //封装网络请求的方法
  request(config: AxiosRequestConfig) {
    return this.instance.request(config); //  使用axios实例发起请求并返回结果
  }
}

export default XLRequest
```

创建实例：

```ts
export const xlRequest2 = new XLRequset({
  baseURL: "http://codercba.com:1888/airbnb/api",
  timeout: 8000,
  interceptors: {
    requestSuccessFn: (config) => {
      console.log("拦截爱彼迎请求成功");
      return config;
    },
    requestFailureFn: (err: any) => {
      console.log("拦截爱彼迎请求失败");
      return err;
    },
    responseSuccessFn: (res) => {
      console.log("拦截爱彼迎响应成功");
      return res;
    },
    responseFailureFn: (err: any) => {
      console.log("拦截爱彼迎响应失败");
      return err;
    },
  },
});
```

发送网路请求：

```ts
xlRequest2.request({
  url: "/home/hotrecommenddest",
}).then(res => {
  console.log(res)
})
```

## 2.3 发送拦截器

```ts
import axios from 'axios' //  引入axios库
//  从axios中导入AxiosInstance和AxiosRequestConfig类型
import {
  AxiosInstance,
  AxiosRequestConfig,
  AxiosResponse,
  InternalAxiosRequestConfig,
} from "axios";

// 自定义接口
interface XLInterceptors {
  // 请求成功拦截
  requestSuccessFn?: (
    config: InternalAxiosRequestConfig
  ) => InternalAxiosRequestConfig;
  // 请求失败拦截
  requestFailureFn?: (err: any) => any;
  // 响应成功拦截
  responseSuccessFn?: (res: AxiosResponse) => AxiosResponse;
  // 响应失败拦截
  responseFailureFn?: (err: any) => any;
}
//定义继承 AxisoRequestConfig 的接口
interface XLRequestConfig extends AxiosRequestConfig {
  interceptors?: XLInterceptors;
}


class XLRequest {
  //  实例变量，用于存储 Axios 实例 AxiosInstance 是 Axios 库中定义的类型，表示一个 Axios 实例的接口
  instance: AxiosInstance;

  //rquest实例 => axios实例
  constructor(config: XLRequestConfig) {
    //  使用传入的配置创建axios实例并保存到当前实例的instance属性中
    this.instance = axios.create(config);

    //全局拦截器
    //  请求拦截器
    this.instance.interceptors.request.use(
      (config) => {
        //  在请求发送之前执行一些操作，例如添加请求头等
        console.log("全局请求成功拦截");
        return config;
      },
      (err) => {
        //  在请求发送失败时执行一些操作
        console.log("全局请求失败拦截");
        return err;
      }
    );
    //  响应拦截器
    this.instance.interceptors.response.use(
      (res) => {
        //  在响应成功时执行一些操作
        console.log("全局响应成功拦截");
        return res;
      },
      (err) => {
        console.log("全局响应失败拦截");
        return err;
      }
    );

    //  如果传入的配置中包含拦截器，则添加到实例中(对爱彼迎特定添加拦截器)
    //  可以添加多个拦截器，拦截器不会覆盖，而是按顺序执行
    this.instance.interceptors.request.use(
      config.interceptors?.requestSuccessFn,
      config.interceptors?.requestFailureFn
    );
    this.instance.interceptors.response.use(
      config.interceptors?.responseSuccessFn,
      config.interceptors?.responseFailureFn
    )

  }

  //封装网络请求的方法
  request(config: XLRequestConfig) {
    if (config.interceptors?.requestSuccessFn) {
      //局部请求成功拦截
      config.interceptors.requestSuccessFn(config as InternalAxiosRequestConfig);
    }
    //返回 Promise，可以通过then得到数据
    return new Promise((resolve, reject) => {
      this.instance.request(config).then(res => {
        if (config.interceptors?.responseSuccessFn) {
          //局部响应成功拦截
          res = config.interceptors.responseSuccessFn(res);
        }
        resolve(res);
      }).catch(err => {
        reject(err)
      })
    })
  }
}

export default XLRequest
```

创建实例：

```ts
export const xlRequest3 = new XLRequset({
  baseURL: "http://codercba.com:1888/airbnb/api",
  timeout: 8000
})
```

发送请求：

```ts
xlRequest3
  .request({
    url: "/home/goodprice",
    interceptors: {
      requestSuccessFn: (config) => {
        console.log("局部精确请求成功拦截")
        return config
      },
      responseSuccessFn: (res => {
        console.log("局部精确响应成功拦截")
        return res
      })
    },
  })
  .then((res) => {
    console.log(res);
  });
```

# 三、添加泛型

**首先要知道为什么要添加泛型**：通过上面的请求方式，我们请求到的是一个 [[03 TS数据类型#二、unknown类型|unknown]] 类型，不可以进行任何操作，那么请求到的数据岂不是毫无用处。

- 首相要解决 unknown 的问题，
- 然后希望得到的数据是**根据返回的数据进行动态的推导的**
- 最后就是更具 **希望得到动态的返回类型**，那么肯定是使用 **泛型** 最好

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17607933630003lb9qf.png)

```ts
import axios from 'axios' //  引入axios库
//  从axios中导入AxiosInstance和AxiosRequestConfig类型
import {
  AxiosInstance,
  AxiosRequestConfig,
  AxiosResponse,
  InternalAxiosRequestConfig,
} from "axios";

// 自定义接口
interface XLInterceptors<T> {
  // 请求成功拦截
  requestSuccessFn?: (
    config: InternalAxiosRequestConfig
  ) => InternalAxiosRequestConfig;
  // 请求失败拦截
  requestFailureFn?: (err: any) => any;
  // 响应成功拦截
  responseSuccessFn?: (res: T) => T;
  // 响应失败拦截
  responseFailureFn?: (err: any) => any;
}
//定义继承 AxisoRequestConfig 的接口
interface XLRequestConfig<T = AxiosResponse> extends AxiosRequestConfig {
  interceptors?: XLInterceptors<T>;
}


class XLRequest {
  //  实例变量，用于存储 Axios 实例 AxiosInstance 是 Axios 库中定义的类型，表示一个 Axios 实例的接口
  instance: AxiosInstance;

  //rquest实例 => axios实例
  constructor(config: XLRequestConfig) {
    //  使用传入的配置创建axios实例并保存到当前实例的instance属性中
    this.instance = axios.create(config);

    //全局拦截器
    //  请求拦截器
    this.instance.interceptors.request.use(
      (config) => {
        //  在请求发送之前执行一些操作，例如添加请求头等
        console.log("全局请求成功拦截");
        return config;
      },
      (err) => {
        //  在请求发送失败时执行一些操作
        console.log("全局请求失败拦截");
        return err;
      }
    );
    //  响应拦截器
    this.instance.interceptors.response.use(
      (res) => {
        //  在响应成功时执行一些操作
        console.log("全局响应成功拦截");
        return res;
      },
      (err) => {
        console.log("全局响应失败拦截");
        return err;
      }
    );

    //  如果传入的配置中包含拦截器，则添加到实例中(对爱彼迎特定添加拦截器)
    //  可以添加多个拦截器，拦截器不会覆盖，而是按顺序执行
    this.instance.interceptors.request.use(
      config.interceptors?.requestSuccessFn,
      config.interceptors?.requestFailureFn
    );
    this.instance.interceptors.response.use(
      config.interceptors?.responseSuccessFn,
      config.interceptors?.responseFailureFn
    )

  }

  //封装网络请求的方法
  request<T = any>(config: XLRequestConfig<T>) {
    if (config.interceptors?.requestSuccessFn) {
      //局部请求成功拦截
      config.interceptors.requestSuccessFn(config as InternalAxiosRequestConfig);
    }
    //返回 Promise，可以通过then得到数据
    return new Promise<T>((resolve, reject) => {
      this.instance.request<any, T>(config).then(res => {
        if (config.interceptors?.responseSuccessFn) {
          //局部响应成功拦截
          res = config.interceptors.responseSuccessFn(res);
        }
        resolve(res);
      }).catch(err => {
        reject(err)
      })
    })
  }
}

export default XLRequest
```

# 四、添加其他请求模式

```ts
import axios from 'axios' //  引入axios库
//  从axios中导入AxiosInstance和AxiosRequestConfig类型
import {
  AxiosInstance,
  AxiosRequestConfig,
  AxiosResponse,
  InternalAxiosRequestConfig,
} from "axios";

// 自定义接口
interface XLInterceptors<T> {
  // 请求成功拦截
  requestSuccessFn?: (
    config: InternalAxiosRequestConfig
  ) => InternalAxiosRequestConfig;
  // 请求失败拦截
  requestFailureFn?: (err: any) => any;
  // 响应成功拦截
  responseSuccessFn?: (res: T) => T;
  // 响应失败拦截
  responseFailureFn?: (err: any) => any;
}
//定义继承 AxisoRequestConfig 的接口
interface XLRequestConfig<T = AxiosResponse> extends AxiosRequestConfig {
  interceptors?: XLInterceptors<T>;
}


class XLRequest {
  //  实例变量，用于存储 Axios 实例 AxiosInstance 是 Axios 库中定义的类型，表示一个 Axios 实例的接口
  instance: AxiosInstance;

  //rquest实例 => axios实例
  constructor(config: XLRequestConfig) {
    //  使用传入的配置创建axios实例并保存到当前实例的instance属性中
    this.instance = axios.create(config);

    //全局拦截器
    //  请求拦截器
    this.instance.interceptors.request.use(
      (config) => {
        //  在请求发送之前执行一些操作，例如添加请求头等
        console.log("全局请求成功拦截");
        return config;
      },
      (err) => {
        //  在请求发送失败时执行一些操作
        console.log("全局请求失败拦截");
        return err;
      }
    );
    //  响应拦截器
    this.instance.interceptors.response.use(
      (res) => {
        //  在响应成功时执行一些操作
        console.log("全局响应成功拦截");
        return res;
      },
      (err) => {
        console.log("全局响应失败拦截");
        return err;
      }
    );

    //  如果传入的配置中包含拦截器，则添加到实例中(对爱彼迎特定添加拦截器)
    //  可以添加多个拦截器，拦截器不会覆盖，而是按顺序执行
    this.instance.interceptors.request.use(
      config.interceptors?.requestSuccessFn,
      config.interceptors?.requestFailureFn
    );
    this.instance.interceptors.response.use(
      config.interceptors?.responseSuccessFn,
      config.interceptors?.responseFailureFn
    )

  }

  //封装网络请求的方法
  request<T = any>(config: XLRequestConfig<T>) {
    if (config.interceptors?.requestSuccessFn) {
      //局部请求成功拦截
      config.interceptors.requestSuccessFn(config as InternalAxiosRequestConfig);
    }
    //返回 Promise，可以通过then得到数据
    return new Promise<T>((resolve, reject) => {
      this.instance.request<any, T>(config).then(res => {
        if (config.interceptors?.responseSuccessFn) {
          //局部响应成功拦截
          res = config.interceptors.responseSuccessFn(res);
        }
        resolve(res);
      }).catch(err => {
        reject(err)
      })
    })
  }

  // 其他网络请求
  get<T = any>(config: XLRequestConfig<T>) {
    return this.request<T>({ ...config, method: 'GET' })
  }
  post<T = any>(config: XLRequestConfig<T>) {
    return this.request<T>({ ...config, method: 'POST' })
  }
  pathch<T = any>(config: XLRequestConfig<T>) {
    return this.request<T>({ ...config, method: 'PATCH' })
  }

  delete<T = any>(config: XLRequestConfig<T>) {
    return this.request<T>({ ...config, method: 'DELETE' })
  }
}

export default XLRequest
```


# 五、总结

上面添加的拦截器：

- 类拦截器就是在创建类的时候就绑定的拦截器，后面使用类的时候都包含这个拦截器，也可以叫全局拦截器。
- 实例拦截器就是在创建实例的时候，编写进行的，后面在使用这个实例的时候都会包含这个拦截器。
- 发送拦截器，就是在实例发送的时候还会创建一个拦截器。

> [!tip] 
> 类拦截器是在创建类的时候创建的，实例拦截器是在创建实例的时候创建的，发送拦截器是在发送网络请求的时候创建的





