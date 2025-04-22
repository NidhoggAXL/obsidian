# 编写App.vue代码
在开发中我们会编写Vue相关的代码，webpack可以对Vue代码进行解析： 

* 接下来我们编写自己的App.vue代码；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744716786000h3e63s.png)

# App.vue的打包过程

我们对代码打包会报错：我们需要合适的Loader来处理文件。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744716805000aexhxx.png)

这个时候我们需要使用vue-loader：

```
npm install vue-loader -D
```

在webpack的模板规则中进行配置：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744716830000g475pt.png)

# @vue/compiler-sfc
打包依然会报错，这是因为我们必须添加@vue/compiler-sfc来对template进行解析：

```
npm install @vue/compiler-sfc -D
```

另外我们需要配置对应的Vue插件：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744716866000l1nz0v.png)

重新打包即可支持App.vue的写法 

另外，我们也可以编写其他的.vue文件来编写自己的组件；

