> [!tip] 重要思路：为什么还要再封装？
> - 当有一天类似域axios的库不在维护了，这个时候项目和axios已经高度耦合了
> - 如果要进行更改，那么整个项目的更改就会变得非常困难与麻烦

封装的方式没有固定的要求，下面就是一种<mark class="hltr-cyan">类的封装思路</mark>。

```js
import axios from 'axios'

class AXLRequest {
  constructor(baseURL, timeout = 10000) {
    //创建新的axios实例
    //为什么不是 this = axios.create 是错误的？
    //如果直接更改this了，那就是this的指向已经改变啦
    //所以就要使用一个this.instance的属性来使用
    //instace - 实例的意思
    this.instance = axios.create({
      baseURL,
      timeout
    })
  }

  request(config) {
    return new Promise((resolve, reject) => {
      //使用axios实例发送请求
      //使用this.instance的属性来使用
      this.instance.request(config).then(res => {
        resolve(res.data)
      }).catch(err => {
        reject(err)
      })
    })
  }

  get(config) {
    return this.request({ ...config, method: "get" })
  }

  post(config) {
    return this.request({ ...config, method: "post" })
  }
}

//使用 new 返回一个实例
export default new AXLRequest("http://123.207.32.32:9001")
```


