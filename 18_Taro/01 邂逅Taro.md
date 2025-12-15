# 一、认识Taro框架

什么是Taro？

 - Taro 是由京东 凹凸实验室 打造的一个开放式跨端、跨框架解决方案，并于2018 年 6 月 7 日正式开源。
 - Taro支持使用 React/Vue/Preact等框架来开发 微信 / 京东 / 百度 / 支付宝 / 字节跳动 / QQ 等小程序 / H5 / RN 等应用。

| 版本系列               | 核心架构      | 发布时间与状态                                                                                                                                                      | 主要特点与里程碑                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------ | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Taro 1.x / 2.x** | **编译时**   | 2018年6月上线[](https://baike.baidu.com/item/taro/23339887?fr=aladdin)。已停止新特性开发，仅修复重大问题[](https://docs.taro.zone/docs/version)。                                  | 初始版本，通过代码编译将类React语法转换为各小程序平台代码。Taro 2.x引入了Webpack重构构建系统[](https://docs.taro.zone/docs/2.x/migrate-to-2/)。                                                                                                                                                                                                                                                                                    |
| **Taro 3.x**       | **运行时**   | 2020年发布，当前仍为迭代重心之一[](https://docs.taro.zone/docs/version)。                                                                                                   | **架构革命**：采用重运行时架构，支持完整的 **React / Vue** 等框架开发体验[](https://docs.taro.zone/docs/version)。**关键版本**：3.1（开放式插件化架构）[](https://docs.taro.zone/docs/version)、3.2（全面支持React Native）[](https://docs.taro.zone/docs/version)[](https://developer.baidu.com/article/details/2888674)、3.3（支持HTML标签开发）[](https://docs.taro.zone/docs/version)、3.4（支持Vue 3.2和Preact）[](https://docs.taro.zone/docs/version)。 |
| **Taro 4.x**       | **运行时增强** | 2024年进入Beta[](https://blog.csdn.net/weixin_48091641/article/details/138110436)，已发布多个稳定版本（如4.1.5[](https://www.oschina.net/news/364028/taro-4-1-5-released)）。 | **支持鸿蒙平台**：核心特性，可通过插件将项目编译为纯血鸿蒙应用[](https://docs.taro.zone/en/blog/2025/05/16/taro-harmony-c-api)[](https://blog.csdn.net/weixin_48091641/article/details/138110436)。**性能与工程优化**：引入Vite、编译模式等优化，并进行依赖库与Node版本升级[](https://www.oschina.net/news/323299/taro-4-0-8-released)[](https://blog.csdn.net/weixin_48091641/article/details/138110436)。                                                |

# 二、Taro的特点

多端支持

 - Taro 3 可以支持转换到 H5、ReactNative 以及任意小程序平台（重心是小程序端）。
 - 目前官方支持转换的平台如下
	 - H5、ReactNative、微信小程序、京东小程序、百度小程序、支付宝小程序、字节跳动小程序
	 - QQ 小程序、钉钉小程序、**企业微信小程序**、支付宝小程序等

多框架支持

 - 在 Taro 3 中可以使用完整的 **React / Vue / Nervjs / Preact** 开发体验

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765798343000fmwun5.png)

# 三、Taro vs uni-app

| 对比维度        | **Taro**                                                                                                                                                                                                                                                                               | **uni-app**                                                                                                                                                                                                                                                                                                                         |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **跨端支持度**   | **核心支持**：小程序（微信/支付宝/百度/字节等）、H5、**React Native (App)**[](https://juejin.cn/post/7559229528632672308)[](https://blog.csdn.net/m0_57108418/article/details/154780672)。  <br>**显著特点**：输出到React Native是特色，适合用React生态开发原生App[](https://blog.csdn.net/m0_57108418/article/details/154780672)。 | **核心支持**：小程序（覆盖最广）、H5、App（WebView/Nvue原生渲染）、快应用[](https://blog.csdn.net/shaobingj126/article/details/154487651)[](https://my.oschina.net/emacs_9268323/blog/18269221)[](https://juejin.cn/post/7559229528632672308)。  <br>**显著特点**：平台覆盖**最广**，尤其是国内小程序；App端可通过`nvue`进行原生渲染[](https://baijiahao.baidu.com/s?id=1839998008495142392)。 |
| **资料完善度**   | 官方文档齐全，社区教程丰富，尤其适合有React/Vue背景的开发者[](https://www.xinlingshou.com/contents/articles/45406.html)[](https://my.oschina.net/emacs_9268323/blog/18269221)。                                                                                                                                  | 官方文档详尽，中文资料（教程、问答、视频）**极其丰富**，对新手非常友好[](https://www.xinlingshou.com/contents/articles/45406.html)[](https://blog.csdn.net/shaobingj126/article/details/154487651)。                                                                                                                                                                  |
| **社区活跃度**   | 社区**非常活跃**，由京东团队维护，在GitHub和中文技术社区有大量开发者[](https://www.xinlingshou.com/contents/articles/45406.html)[](https://my.oschina.net/emacs_9268323/blog/18269221)[](https://juejin.cn/post/7559229528632672308)。                                                                               | 社区**极为活跃**，拥有可能是国内最大的跨端开发者社区，问题反馈和解决方案获取迅速[](https://www.xinlingshou.com/contents/articles/45406.html)。                                                                                                                                                                                                                             |
| **工具与周边生态** | **构建工具**：支持Webpack和Vite，**工程化配置灵活**[](https://juejin.cn/post/7559229528632672308)。  <br>**UI库**：有`NutUI`（京东风格）等，但选择相对较少。  <br>**特点**：深度集成**React/Vue生态**，可复用其海量第三方库[](https://juejin.cn/post/7559229528632672308)[](https://blog.csdn.net/m0_57108418/article/details/154780672)。      | **开发工具**：官方提供**HBuilderX**，内置调试、打包、真机运行等功能，**开箱即用**[](https://www.xinlingshou.com/contents/articles/45406.html)[](https://juejin.cn/post/7559229528632672308)。  <br>**插件市场**：拥有**极其丰富**的官方插件市场，涵盖功能封装、UI组件、项目模板[](https://juejin.cn/post/7559229528632672308)。                                                                      |

## 💡 如何选择：Taro 还是 uni-app？

你的选择应回归到**团队技术栈**和**项目核心需求**：

1. **选择 Taro，如果你的团队**：
    
    - **技术栈是 React**：希望用React/Vue开发，并需要将代码输出到**React Native App**，追求更灵活的工程化配置。
        
    - **项目类型**：可能是**中大型应用**、电商项目，或需要与现有React技术栈深度集成。
        
2. **选择 uni-app，如果你的团队**：
    
    - **技术栈是 Vue** 或**追求最高开发效率**：希望利用丰富的插件市场和HBuilderX工具快速开发。
        
    - **项目需求**：需要覆盖**尽可能多的平台**（尤其是各类小程序），或是**中小型项目**、内容/工具型应用。
        

总的来说，uni-app在**平台覆盖广度、开发工具链和开箱即用生态**上优势明显；而Taro在**技术栈灵活性、与现代前端工程化融合以及React Native输出**方面更胜一筹。

# 四、Taro架构图

Taro 当前的架构主要分为：编译时 和 运行时。

其中编译时主要是将 Taro 代码通过 Babel  转换成 小程序的代码，如：JS、WXML、WXSS、JSON。 

运行时主要是进行一些：生命周期、事件、data 等部分的处理和对接，以保证和宿主平台数据的一致性。

# 五、编辑器选择

我们推荐使用 [VSCode](https://code.visualstudio.com/) 或 [WebStorm](https://www.jetbrains.com/webstorm/)（或其它支持 Web 开发的 Jetbrains IDE）。

当你使用 VSCode 时，推荐安装 [ESLint 插件](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)，如果你使用 TypeScript，别忘了配置 `eslint.probe` 参数。如果使用 Vue，推荐安装 [Vetu(Vue2)](https://marketplace.visualstudio.com/items?itemName=octref.vetur) 或者 **Valor(Vue3)** 插件。

如果你愿意花钱又懒得折腾可以选择 [WebStorm](https://www.jetbrains.com/webstorm/)（或其它支持 Web 开发的 Jetbrains IDE），基本不需要配置。

不管使用 VSCode 还是 WebStrom，安装了上述插件之后使用 Taro 都实现自动补全和代码实时检查（linting）的功能。
