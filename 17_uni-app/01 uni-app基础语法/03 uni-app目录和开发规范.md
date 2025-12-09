# 一、目录结构

| 文件/目录                       | 主要作用                                                                              |
| --------------------------- | --------------------------------------------------------------------------------- |
| **pages/**                  | 存放所有**业务页面**的目录，每个页面通常是一个单独的文件夹，内含 `.vue` 文件。                                     |
| **static/**                 | 存放**静态资源**，如图片、字体等。此目录下的文件会直接复制到最终发布包中。                                           |
| **components/**             | 存放**可复用的Vue组件**。                                                                  |
| **uni_modules/**            | 存放通过官方插件市场安装的**uni_modules插件**。                                                   |
| **unpackage/**              | **编译生成目录**，存放各平台（如小程序、App）的编译结果，此目录不应提交至代码仓库。                                     |
| **App.vue**                 | **应用根组件和全局配置**，用于设置全局样式、监听应用生命周期。                                                 |
| **main.js**                 | **Vue应用入口文件**，负责初始化Vue实例并加载应用配置。                                                  |
| **pages.json**              | **页面路由与全局样式配置文件**，用于设置页面路径、窗口外观、导航栏、底部Tab栏等。                                      |
| **manifest.json**           | **应用配置文件**，配置App ID、名称、图标、启动图、SDK配置等与打包相关的信息。                                     |
| **index.html**              | Web端的**主页入口文件**。                                                                  |
| **uni.scss**                | **预置的全局样式变量文件**，方便统一管理主题颜色、边框等样式。                                                 |
| **ni.promisify.adaptor.js** | **异步API转换适配器**。用于将微信小程序等平台**传统的回调风格API转换为Promise风格**，方便开发者使用 `async/await` 进行异步编程 |

## 📁 核心目录详解

一个功能完整的项目通常会包含以下目录：

- **`pages/`**：这是你开发工作的核心。每个子目录（如 `pages/index/`）代表一个页面，其中必须包含一个 `.vue` 文件（如 `index.vue`）作为页面组件[](https://uniapp.dcloud.io/tutorial/project.html#%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84)。页面路径需要在 `pages.json` 中注册。
    
- **`components/`**：为了提高代码复用性，应将可复用的界面模块（如按钮、导航栏、卡片）抽取为Vue组件放在这里[](https://bbs.huaweicloud.com/blogs/442051)。
    
- **`static/`**：项目所有的本地静态资源都应放在这里[](https://uniapp.dcloud.io/tutorial/project.html#%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84)。在代码中，可以使用绝对路径（如 `/static/logo.png`）或相对路径引用它们[](https://uniapp.dcloud.net.cn/tutorial/page-static-assets.html)。需要注意，此目录内容会直接拷贝到最终产物中，要避免存放未使用的大文件。
    
- **`uni_modules/`**：当你从uni-app插件市场安装符合 `uni_modules` 规范的组件或库时，它们会存放在这里，通常可以按需引入，非常方便。
    
- **`unpackage/`**：这是HBuilder X编译后自动生成的目录，里面是准备发布到各端（如微信小程序、App）的代码包[](https://bbs.huaweicloud.com/blogs/442051)。这个目录应当被 `.gitignore` 忽略。
    

## 📄 核心文件详解

- **`App.vue`**：这是应用的“外壳”。你可以在 `<style>` 标签内编写所有页面共享的全局CSS样式。更重要的是，你可以在这里使用Vue的生命周期函数来监听**应用级别**的事件，例如应用启动、切换到后台等。
    
- **`main.js`**：是整个应用的启动引擎。它创建Vue实例，并引入和挂载 `App.vue` 组件。你通常也会在这里注册需要全局使用的库或组件。
    
- **`pages.json`**：这是uni-app的“路由和导航说明书”。它最主要的功能有两个：
    
    1. **配置页面路由**：通过 `pages` 数组设置每个页面的访问路径和基础样式。
        
    2. **配置全局导航**：定义整个应用的窗口背景色、导航栏标题样式 (`globalStyle`)，以及如果需要，可以配置原生的底部 `tabBar` 导航栏。
        
- **`manifest.json`**：这是应用打包前的“产品说明书”。当你需要为不同平台（如微信小程序、Android App）生成安装包时，就需要在这里配置该平台特有的信息，比如小程序的AppID、App的启动图、应用所需的系统权限列表等。


### uni.promisify.adaptor.js 详解

这个文件通常在你创建项目后静默存在于根目录。为了帮你快速理解，其核心信息如下：

|项目|说明|
|---|---|
|**主要作用**|**异步API转换适配器**。用于将微信小程序等平台**传统的回调风格API转换为Promise风格**，方便开发者使用 `async/await` 进行异步编程[](https://ask.csdn.net/questions/8069918)[](https://blog.csdn.net/Zmaomao_/article/details/140465750)[](https://bbs.itying.com/topic/678e68c54b218c005fa26469)。|
|**典型使用场景**|当你需要调用 `wx.request()`、`wx.getLocation()` 等小程序原生API，并希望用Promise处理时，这个文件在底层提供支持。|
|**是否可以删除**|**视情况而定**，但有风险：  <br>1. **可以删除**：如果你的项目完全不使用微信小程序的异步API，或确定所有异步调用都已使用uni-app封装的、本身就返回Promise的API（如 `uni.request`），那么**理论上可以删除**[](https://ask.csdn.net/questions/8069918)[](https://blog.csdn.net/Zmaomao_/article/details/140465750)。  <br>2. **不建议删除**：如果你或你引入的第三方库依赖了此转换功能，删除后可能导致程序运行出错[](https://bbs.itying.com/topic/678e68c54b218c005fa26469)。最稳妥的做法是**保留它**，因为它体积很小，不影响打包。|
|**官方地位**|它更像是一个**构建时或运行时的内部适配文件**。在DCloud官方最新的工程结构文档中，并未将此文件列为必需或标准文件[](https://uniapp.dcloud.io/tutorial/project.html#%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84)，这可能是不同HBuilderX模板版本或项目配置的差异所致。|

# 二、开发规范


了实现多端兼容，综合考虑编译速度、运行性能等因素，uni-app 约定了如下开发规范：

- 页面文件遵循 Vue 单文件组件 (SFC) 规范
- 组件标签靠近小程序规范，详见 uni-app 组件规范
- 接口能力（JS API）靠近微信小程序规范，但需将前缀 wx 替换为 uni，详见uni-app接口规范
- 数据绑定及事件处理同 Vue.js 规范，同时补充了App及页面的生命周期
- 为兼容多端运行，建议使用flex布局进行开发，**推荐使用rpx单位（750设计稿）**。
- 文档直接查看uni-app的官网文档： https://uniapp.dcloud.net.cn/


# 三、main.js


main.js是 uni-app 的入口文件，主要作用是：

- 初始化vue实例。
- 定义全局组件。
- 定义全局属性。
- 安装插件，如：pinia、vuex 等。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765248783000ts8ke5.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765248788000p8c0km.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765248810000ts5hje.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765248825000latb6b.png)

# 四、App.vue

App.vue入口组件

- App.vue是uni-app的入口组件，所有页面都是在App.vue下进行切换
- App.vue本身不是页面，这里不能编写视图元素，也就是没有`<template>`元素

App.vue的作用：

- 应用的生命周期
- 编写全局样式
- 定义全局数据 globalData

> [!tip]
> 
> 注意：应用生命的周期仅可在App.vue中监听，在页面监听无效。

![gh|400](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17652489850009rmn3q.png)


# 五、全局和局部样式

全局样式:

- App.vue 中style的样式为全局样式，作用于每一个页面（**style标签不支持scoped，写了导致样式无效**）。
	- App.vue 中通过 `@import` 语句可以导入外联样式，一样作用于每一个页面。
- uni.scss 文件也是用来编写全局公共样式，通常用来定义全局变量。
	- uni.scss 中通过 `@import` 语句可以导入外联样式，一样作用于每一个页面。

```css
@import "@/static/css/global.scss";
```


局部样式

- 在 pages 目录下 的 vue 文件的style中的样式为局部样式，只作用对应的页面，并**会覆盖 App.vue 中相同的选择器**。
- vue文件中的style标签也可支持scss等预处理器，比如：安装dart-sass插件后，style标签便可支持scss写样式了。
- style标签支持scoped吗？**不支持**，不需写。

```css
<style lang="scss"></style>
```


# 六、uni.scss

uni.scss 全局样式文件

- 为了方便整体控制应用风格。 默认定义了uni-app框架内置全局变量，当然也可以存放自定义的全局变量等
- 在uni.scss中定义的变量，我们**无需 `@import` 就可以在任意组件中直接使用。**
- 使用uni.scss中的变量，需在 HBuilderX 里面安装 scss 插件（dart-sass插件），
- 然后在该组件的 style 上加 lang=“scss”，重启即可生效。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765249368000ivzntp.png)

> [!tip] 注意事项：
> 
>  - 这里的**uni-app框架**内置变量和后面**uni-ui组件库**的内置变量是不一样的。 
>  - uni.scss定义的变量是全局可以直接使用，App.vue定义的变量只能在当前组件中使用。

# 七、页面调用接口

getApp() 函数( 兼容h5、weapp、app )：用于获取**当前应用实例**，可用于获取globalData 。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765249848000jcbeuh.png)


getCurrentPages() 函数( 兼容h5、weapp、app )

- 用于获取当前**页面栈的实例**，以数组形式按栈的顺序给出。
	- 数组：第一个元素为首页，最后一个元素为当前页面。
- 仅用于展示页面栈的情况，请勿修改页面栈，以免造成页面状态错误。
- 常用方法如下图所示：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17652498600001s5wl9.png)

# 八、page.json

page.json全局页面配置（兼容h5、weapp、app ）

- pages.json 文件用来对 uni-app 进行全局配置，**类似微信小程序中app.json**。
- 决定页面的路径、窗口样式、原生的导航栏、底部的原生tabbar 等。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765250232000pprvek.png)

# 九、manifest.json

manifest.json应用配置

- Android平台相关配置
- iOS平台相关配置
- Web端相关的配置
- 微信小程序相关配置
	- wxbc30134b589795b0
- ....

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765250284000e4c5mv.png)

