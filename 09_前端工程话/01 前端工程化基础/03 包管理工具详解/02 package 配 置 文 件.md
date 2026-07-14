# 一、npm 的配置文件

那么对于一个项目来说，我们如何使用**npm来管理这么多包**呢?

* 事实上，我们每一个项目都会有一个对应的**配置文件**，无论是前端项目(Vue、React)还是后端项目(Node);
* 这个配置文件会记录着你**项目的名称、版本号、项目描述**等;
* 也会记录着你项目**所依赖的其他库的信息和依赖库的版本号**

**这个配置文件就是package.json**

那么这个配置文件如何得到呢?

* 方式一:**手动从零创建项目**，npm init -y
	* 使用默认配置文件内容

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744111378000rlwlzp.png)

* 方式三：通过 npm init 
	* 每一步都输入配置信息

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744111491000g2bxdu.png)


* 方式二:通过脚手架创建项目，脚手架会帮助我们生成package.json，并且里面有相关的配置

# 二、常见的配置文件

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17441117150006d76o3.png)

# 三、常见的属性
## 3.1 name、version 

必须填写的属性：name、version 

* name是项目的名称； 
* version是当前项目的版本号； 
* description是描述信息，很多时候是作为项目的基本描述； 
* author是作者相关信息（发布时用到）； 
* license是开源协议（发布时用到）；

## 3.2 private(私有)

private属性： 

* private属性记录当前的项目是否是私有的； 
* **当值为true时，npm是不能发布它的**，这是防止私有项目或模块发布出去的方式；

## 3.3 main(主要)

main属性： 

* 设置程序的入口。 
* 比如我们使用axios模块 `const axios = require('axios');` 
* 如果有main属性，实际上是找到对应的main属性查找文件的；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744112533000pji6ei.png)

## 3.4 所有类型的 scripts(脚本)

**scripts属性：** 

* **scripts属性用于配置一些脚本命令，以键值对的形式存在；** 
* 配置后我们可以通过 npm run 命令的key来执行这个命令； 
* npm start和npm run start的区别是什么？ 
	* 它们是等价的； 
	* 对于常用的 start、 test、stop、restart可以**省略掉run**直接通过 npm start等方式运行；

![gh|700](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744114255000o3dp53.png)

**dependencies(依赖项)属性：** 

* dependencies属性是指定**无论开发环境还是生成环境都需要依赖的包**； 
* 通常是我们**项目实际开发用到的一些库模块vue、vuex、vue-router、react、react-dom、axios**等等； 
* 与之对应的是devDependencies；

**devDependencies(开发依赖)属性：**

* 一些包在生成环境是不需要的，比如webpack、babel等； 
* 这个时候我们会通过 `npm install webpack --save-dev`，将它安装到devDependencies属性中；
	* 也可以简写为 `npm install webpack -D`


> [!tip] 开发环境和生成环境
> ![[开发环境和生成环境|500]]

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744115050000jf19jk.png)


peerDependencies属性：

* 还有一种项目依赖关系是**对等依赖**，也就是**你依赖的一个包**，它必须是**以另外一个宿主包为前提的**； 
* 比如element-plus是依赖于vue3的，ant design是依赖于react、react-dom；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744115294000fqu0zr.png)


# 四、依赖版本管理

我们会发现安装的依赖版本出现:^2.0.3或~2.0.3，这是什么意思呢?

npm的包通常需要遵从semver版本规范:

- semver: https://semver.org/lang/zh-CN/anpm 
- semver:https://docs.npmjs.com/misc/semver

**semver版本规范是X.Y.Z:**

- X主版本号(major)当你做了不兼容的 API修改(可能不兼容之前的版本)当你做了向下兼容的功能性新增(新功能增加，但是兼容之前的版本)
- Y次版本号(minor)当你做了向下兼容的问题修正(没有新功能，修复了之前版本的bug);
- Z修订号(patch)

**我们这里解释一下 `^` 和 `~` 的区别:**

 - **`x.y.z`**:表示一个明确的版本号
- **`^x.y.z`**:表示x是保持不变的，y和z永远安装最新的版本
- **`~x.y.z`**:表示x和y保持不变的，z永远安装最新的版本

## 4.1 常见属性(了解)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744116301000d5hlhq.png)




