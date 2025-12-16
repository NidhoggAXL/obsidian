# 一、组件及生命周期

在 Taro中，除了应用和页面组件有生命周期之外， **Taro 的组件也是生命周期**，如下图所示：

下面我们来编写一个HYButton组件。

 - 创建组件
 - 定义属性
 - 样式编写
 - 定义插槽
 - 定义生命周期
 - 组件可编写页面生命周期吗？
	 - class组件默认不行，需要单独处理
	 - 但是函数组件是支持的
 - 页面可以编写组件生命周期吗？可以

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765890807000cvfzu3.png)

为了后面方便使用需要先安装两个库：[[07 classnames库使用|classnames]]、protypes

```bash
yarn install classnames

yarn install proptypes
```

