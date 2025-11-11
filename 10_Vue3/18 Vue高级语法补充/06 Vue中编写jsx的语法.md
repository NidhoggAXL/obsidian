# 一、jsx的babel配置

如果我们希望在项目中使用jsx，那么我们需要添加对jsx的支持： 

* jsx我们通常会**通过Babel来进行转换**（React编写的jsx就是通过babel转换的）； 
* 对于Vue来说，我们只需要在Babel中**配置对应的插件**即可；

## 1.1 vue CLI环境

安装Babel支持Vue的jsx插件：

```bash
npm install @vue/babel-plugin-jsx -D
```

在babel.config.js配置文件中配置插件：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753414105000dnxsgz.png)

## 1.2 vite环境

```bash
npm install @vitejs/plugin-vue-jsx -D
```

## 1.3 使用

在返回时，在（）里面编写元素标签

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/175341426200001wjrh.png)
	
# 二、计数器案例

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753414198000kqayo9.png)

