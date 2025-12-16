# 一、安装

Taro 项目基于 node，请确保已具备较新的 **node 环境（>=12.0.0）**

Taro CLI 工具安装

 - 首先，你需要使用 npm 或者 yarn 全局安装 @tarojs/cli，或者直接使用 npx（如下图所示）:

```bash
npm i –g @tarojs/cli
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765800999000eviapv.png)


查看 Taro CLI 工具版本

```bash
npm info @tarojs/cli
```


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17658011310009f401t.png)


# 二、项目初始化

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765803463000182tzf.png)


安装依赖：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765803483000rpcjz8.png)

# 三、初始化常见错误

因为 Taro 更新频率比较高，所有官方的模板中也回存在错误，需要把错误进行解决，下面是常见的错误

## no-undef

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765803792000xkh8fi.png)

第一种方式：使用 eslink 的注释快速解决，点击快速修复： 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765803854000pmbtle.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176580386400099z1m4.png)

第二种方式：全局取消 eslink 对于no-undef 的检测。

```json title=".eslintrc"
{
  "extends": ["taro/react"],
  "rules": {
    "react/jsx-uses-react": "off",
    "react/react-in-jsx-scope": "off",
    "jsx-quotes": "off",
    "no-undef": "off"//取消全局 no-undef
  }
}
```

> [!tip]
> 这样有一个坏处，就是当其他的函数，如果我们没有定义的时候，就进行使用啦，那么 eslink 就不会进行报错啦。

第三种方式：全局注册这些函数

```json title=".eslintrc"
{
  "extends": ["taro/react"],
  "rules": {
    "react/jsx-uses-react": "off",
    "react/react-in-jsx-scope": "off",
    "jsx-quotes": "off",
    "no-undef": "off"//取消 no-undef
  },
  "globals": {
    "definePageConfig": "readonly"// 只可以读取
  }
}

```

## CommonJS

不可以使用 ComminJS 语法：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765804239000qzq153.png)

关闭 eslint 的检测：

```json title=".eslintrc"
{
  "extends": ["taro/react"],
  "rules": {
    "import/no-commonjs": "off",
}
```


# 三、编译运行

Taro 编译分为 dev 和 build 模式：

 - dev 模式（增加 --watch 参数） 将会监听文件修改。
 - build 模式（去掉 --watch 参数） 将不会监听文件修改，并会对代码进行压缩打包。

dev 命令 启动 Taro 项目的开发环境

 - pnpm run dev:h5 启动H5端
 - pnpm run dev:weapp 启动小程序端

build 命令可以把 Taro 代码编译成不同端的代码，然后在对应的开发工具中查看效果，比如：

 - H5直接在浏览器中可以查看效果
 - 微信小程序需在《微信开发者工具》打开根目录下的dist查看效果
 - RN应用需参考《React Native端开发流程》
 - 等等

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765804689000urgbm8.png)

# 四、目录结构

```text
├── babel.config.js             # Babel 配置
├── .eslintrc.js                # ESLint 配置
├── config                      # 编译配置目录
│   ├── dev.js                  # 开发模式配置
│   ├── index.js                # 默认配置
│   └── prod.js                 # 生产模式配置
├── package.json                # Node.js manifest
├── dist                        # 打包目录
├── project.config.json         # 小程序项目配置
├── src # 源码目录
│   ├── app.config.js           # 全局配置
│   ├── app.css                 # 全局 CSS
│   ├── app.js                  # 入口组件
│   ├── index.html              # H5 入口 HTML
│   └── pages                   # 页面组件
│       └── index
│           ├── index.config.js # 页面配置
│           ├── index.css       # 页面 CSS
│           └── index.jsx       # 页面组件，如果是 Vue 项目，此文件为index.vue
```

# 五、Taro、React开发规范

了实现多端兼容，综合考虑编译速度、运行性能等因素，Taro可以约定了如下开发规范：

 - 页面文件遵循 **React组件 (JSX) 规范**。
 - **组件标签**靠近小程序规范（但**遵从大驼峰，并需导包**），详见Taro [组件规范](https://uniapp.dcloud.net.cn/component/)
 - **接口能力**（JS API）靠近微信小程序规范，但需将**前缀 wx 替换为 Taro(需导包)**，详见Taro[接口规范](https://uniapp.dcloud.net.cn/api/)
 - 数据绑定及事件处理同 React 规范，同时**补充了App及页面的生命周期**
 - 为兼容多端运行，建议使用**flex布局**进行开发，推荐使用 **px 单位（750设计稿）**。
 - 在 React 中使用Taro内置组件前，必须从 **`@tarojs/components`** 进行引入。
 - 文档直接查看Taro的官网文档： https://docs.taro.zone/docs


