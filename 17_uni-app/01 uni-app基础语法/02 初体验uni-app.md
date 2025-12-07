# 一、认识uni-app

官网对uni-app的介绍：

- uni-app 是一个使用 **Vue.js** 开发前端应用的框架。
- 即开发者**编写一套代码，便可发布到iOS、Android、Web（响应式）、以及各种小程序**（微信/支付宝/百度/头条/飞书/QQ/快手/钉钉/淘宝）、快应用等多个平台。
- uni-app在手，做啥都不愁。即使不跨端， **uni-app也是更好的小程序开发框架、更好的App跨平台框架、更方便的H5开发框架**。不管领导安排什么样的项目，你都可以快速交付，不需要转换开发思维、不需要更改开发习惯。

uni-app的历史

- uni-app中的 uni，读 you ni，是统一的意思。
- DCloud于2012年开始研发的小程序技术，并推出了 HBuilder X 开发工具。
- 2015年，DCloud正式商用了自己的小程序，产品名为“流应用”，
	- 并捐献给了工信部旗下的**HTML5中国产业联盟。**
- 该应用能接近原生功能和性能的App，并且即点即用，不需要安装。
- 微信团队经过分析，于2016年初决定上线**微信小程序**业务，**但其没有接入中国产业联盟标准，而是订制了自己的标准**。


# 二、uni-app VS 微信小程序

uni-app和微信小程序相同点：

- 都是**接近原生的体验、打开即用、不需要安装**
- 都可开发微信小程序、都有非常完善的官方文档

uni-app和微信小程序区别：

- **uni-app支持跨平台，编写一套代码，可以发布到多个平台，而微信小程序不支持**
- uni-app纯Vue体验、高效、统一、工程化强，微信小程序工程化弱、使用小程序开发语言。
- 微信小程序适合较复杂、定制性较高、兼容和稳定性更好的应用
- uni-app适合不太复杂的应用，因为需要兼容多端，多端一起兼容和适配增加了开发者心智负担

> [!abstract] uni-app 和 微信小程序，应该如何选择？
> 
> - **需要跨平台、不太复杂的应用选 uni-app**，复杂的应用使用uni-app反而增加了难度。
> - 不需要跨平台、较复杂、对兼容和稳定性要求高的选原生微信小程序。
> 

# 三、uni-app 架 构 图

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765022177000hi4deg.png)


# 四、uni-app初体验

创建uni-app项目：支持 **可视化界面** 和 **Vue-CLI** 两种方式。可视化方式比较简单，HBuilder X 内置相关环境，开箱即用。

开发工具 HBuilder X： Hbuilder X 是通用的前端开发工具，但为 uni-app 做了特别强化 。

- 下载地址：https://hx.dcloud.net.cn/Tutorial/install/windows
- 安装完之后可以注册一个Dcloud的开发者账号(左下角可以点击注册)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765026898000w0y2m4.png)

## 4.1 方式一(推荐)

方式一（推荐）：HBuilderX创建 uni-app项目步骤： 

- 点工具栏里的文件 -> 新建 -> 项目（快捷键Ctrl+N） 
- 选择uni-app类型，输入工程名，选择模板，**选择Vue版本**，点击创建即可。


## 4.2 方式二

方式二： Vue-CLI 命令行创建

创建 vue3 项目：

创建以 javascript 开发的工程（如命令行创建失败，请直接访问  [gitee](https://gitee.com/dcloud/uni-preset-vue/repository/archive/vite.zip) 下载模板）

```bash
npx degit dcloudio/uni-preset-vue#vite 项目名称
```

```bash
npx degit dcloudio/uni-preset-vue#vite-alpha 项目名称
```

创建以 typescript 开发的工程（如命令行创建失败，请直接访问  [gitee](https://gitee.com/dcloud/uni-preset-vue/repository/archive/vite-ts.zip) 下载模板）

```bash
npx degit dcloudio/uni-preset-vue#vite-ts my-vue3-project
```

- 创建 vue2 项目

> [!tip]
> 
> 需要全局安装 vue-cli `npm install -g @vue/cli`

- 使用正式版（对应HBuilderX最新正式版）

```bash
vue create -p dcloudio/uni-preset-vue my-project
```


- 使用alpha版（对应HBuilderX最新alpha版）

```bash
vue create -p dcloudio/uni-preset-vue#alpha my-alpha-project
```

此时，会提示选择项目模板（使用Vue3/Vite版不会提示，目前只支持创建默认模板），初次体验建议选择 `hello uni-app` 项目模板，如下所示：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17650272400001xjz69.png)

# 五、HBuilder X 开发工具特点

HBuilderX从v3.2.5(包含)开始优化了对vue3的支持。

- 完善的提示，在代码助手右侧还能看到清晰的帮助描述。
- 支持css中使用v-bind提示和参数变量提示及转到定义(Alt+click)
- **Vue3推荐使用的setup语法糖支持也完全支持。**
- 在data、props和setup中定义的变量以及methods和setup内定义的函数都能在template中提示和转到定义(Alt+click)。

 HBuilderX支持各种表达式语法，如**less、scss、stylus、typescript**等高亮，无需安装插件。

**this的精准识别和语法提示。**

**组件的标签、属性都可以直接被提示出来。**

不管是关闭HBuilder，还是断电、崩溃，临时文件始终会自动保存。

更多功能：https://hx.dcloud.net.cn/Tutorial/Language/vue


# 六、运行uni-app

## 6.1 web端

在浏览器运行：选中uniapp 项目，点击工具栏的运行 -> 运行到浏览器 -> 选择浏览器，即可体验 uni-app 的 web 版。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17650274080009a40af.png)

> [!tip] 
> 
> 如果打不开，那就要设置浏览器的安装位置，这样才可以正常运行


## 6.2 微信开发者工具

选中uniapp项目，点击工具栏的运行 -> 运行到小程序模拟器 -> 微信开发者工具，即可在微信开发者工具里面体验 uni-app。

其它注意事项：

1. 微信开发者工具需要开启服务端口：小程序开发工具设置 -> 安全（**目的是让HBuilder可以启动微信开发者工具**）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765028244000lj908o.png)


2. 如第一次使用，需配置微信开发者工具的安装路径（会提示下图）。
	- 点击工具栏运行 -> 运行到小程序模拟器 -> 运行设置，配置相应小程序开发者工具的安装路径

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765029330000cqlyw5.png)


3. 自动启动失败，可用微信开发者工具手动打开项目（项目在unpackage/dist/dev/mp-weixin路径下）。

![gh|400](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765029356000askeqh.png)

## 6.3 手机

### 安装mumu模拟器

第一步：下载mumu模拟器：https://mumu.163.com/mac/index.html

第二步：安装mumu模拟器

第三步：配置adb调试桥命令行工具（用于 HBuilder X 和Android模拟器建立连接，来实时调试和热重载。HBuilder X 是有内置adb的 )

- HBuilderX正式版的adb目录位置：安装路径下的 tools/adbs 目录
	- 而MAC下为HBuilderX.app/Contents/tools/adbs目录；
- HBuilderX Alpha版的adb目录位置：安装路径下的 plugins/launcher/tools/adbs 目录( 需先运行后安装了插槽才会有该目录 )
	- 而MAC下为/Applications/HBuilderX-Alpha.app/Contents/HBuilderX/plugins/launcher/tools/adbs目录
- 在adbs目录下运行./adb ，即可使用adb命令（Win和Mac一样）。
- 如想要全局使用 adb 命令，window电脑可在：设置 -> 高级设计 -> 环境变量中设置

第四步：HBuilder X 开发工具连接mumu模拟器，使用adb调试桥来连接

- adb connect 127.0.0.1:7555 （ 端口是固定的，启动mumu模拟器默认是运行在7555端口）

第五步：选中项目 -> 运行 ->运行App到手机或模拟器-> 选中Android基座（基座其实是一个app壳）


### 6.3.1 模拟器

在运行App到手机或模拟器（需要先安装模拟器） 

- 选中uniapp项目，点击工具栏的运行 -> 运行App到手机或模拟器， 
	- 即可在该设备里面体验uni-app（支持中文路径）。


> [!tip]
> 需要使用的adb的目录的时候，一定要先在HBulder X中下载插件，如果是第一次可以点击下面图片所示位置，自动下载插件。
> 
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765105124000by0shi.png)


下载号插件后，打开手机的模拟器，再次点击 `运行到Android App基座(D)` 就可以看到下面的界面：HBulder X会自动识别现在可以使用的模拟器，点击运行就可以把当前项目运行到模拟器上面。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765105254000sjzp35.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17651054020007llcyj.png)

### 6.3.2 WIFI链接Android真机

https://uniapp.dcloud.net.cn/tutorial/run/run-app-android-wifi.html#hbuilderx-4-71-%E7%9A%84%E6%96%B9%E6%A1%88

### 6.2.3 其他的模拟器看移动端开发文件
