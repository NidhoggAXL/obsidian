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


