# 一、编写App.vue代码

在开发中我们会编写Vue相关的代码，webpack可以对Vue代码进行解析： 

* 接下来我们编写自己的App.vue代码；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744716786000h3e63s.png)

# 二、App.vue的打包过程

我们对代码打包会报错：我们需要合适的Loader来处理文件。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744716805000aexhxx.png)

这个时候我们需要使用vue-loader：

```bash
npm install vue-loader -D
```

在webpack的 [[04 编写和打包CSS文件#四、loader配置方式|模板规则]] 中进行配置：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744716830000g475pt.png)

# 三、@vue/compiler-sfc

打包依然会报错，这是因为我们必须添加 @vue/compiler-sfc 来对template进行解析：

```bash
npm install @vue/compiler-sfc -D
```

另外我们需要配置对应的Vue插件：

```js
const { VueLoaderPlugin } = require('vue-loader/dist/index);

module.exports = {
  plugins: [
    new VueLoaderPlugin()
  ]
}
```

> [!tip]
> 重新打包即可支持App.vue的写法 
> 另外，我们也可以编写其他的.vue文件来编写自己的组件；

