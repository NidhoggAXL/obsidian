# 一、require细节
我们现在已经知道，**require是一个函数**，可以帮助我们引入一个文件(模块)中导出的对象。

那么，require的查找规则是怎么样的呢?

* 这里我总结比较常见的查找规则:
* 导入格式如下:require(X)

## 1.1 情况一
情况一:X是一个Node核心模块，比如path、http

直接返回核心模块，并且停止查找

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743838527000lgdtwf.png)


## 1.2 情况二
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743838720000u4e1mo.png)

## 1.3 情况三
情况三:直接是一个X(没有路径)，并且X不是一个核心模块

例如下面代码
```js
requrire("axl")
```

查找顺序如下：

![[require情况三查找顺序|1200]]

如果查找到根目录（最上层目录还是没有，那么就会报错：not found）

> [!tip] 开发中常见的
>```js
>npm install axios
>```
>就是在当前目录下载 axios 源码（如果没有 node_modules 会自动添加这个文件）到 node_modules 文件中。

如果没有 node_modules 的时候：

* 下载中：![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174384161000099jk22.png)
* 下载完（会自动添加 node_modules）：![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743841654000tzculd.png)

# 二、模块的加载过程
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743843115000jnfe08.png)




