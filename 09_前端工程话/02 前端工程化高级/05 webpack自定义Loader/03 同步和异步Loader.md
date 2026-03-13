# 一、同步Loader

什么是同步的Loader呢？

 - 默认创建的Loader就是同步的Loader；
 - 这个Loader必须通过 return 或者 this.callback 来返回结果，交给下一个loader来处理；
 - 通常在有错误的情况下，我们会使用 this.callback；

this.callback的用法如下：

 - 第一个参数必须是 Error 或者 null；
 - 第二个参数是一个 string或者Buffer；

```js
module.exports = function (content, map, meta) {
  console.log("loaders03:", content)
  this.callback(null, content)
}
```

# 二、异步的Loader

什么是异步的Loader呢？

 - 有时候我们使用Loader时会进行一些异步的操作；
 - 我们希望在异步操作完成后，再返回这个loader处理的结果；
 - 这个时候我们就要使用异步的Loader了；

loader-runner已经在执行loader时给我们提供了方法，让loader变成一个异步的loader：

```js
module.exports = function (content, map, meta) {
  const callback = this.async()
  setTimeout(() => {
    console.log("loader03", content)
    callback(null, content)
  }, 2000);
}
```

