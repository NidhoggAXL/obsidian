# 一、Node.js的安装
Node.js是在2009年诞生的，2022年5月目前最新的版本是分别是LTS16.15.1以及Current18.4.0:

* **LTS版本**:(Long-term support,长期支持)相对稳定一些，推荐线上环境使用该版本;
* **Current版本**:最新的Node版本，包含很多新特性;

我们如何选择什么版本呢?

* 如果你是学习使用，可以选择current版本;
* 如果你是 **公司开发**，建议选择 **LTS版本**(面向工作，选择LTS版本)

Node的安装方式有很多:

* 可以借助于一些操作系统上的软件管理工具，比如Mac上的homebrew，Linux上的yum、dnf等;
* 也可以直接下载对应的安装包下载安装

我们选择下载安装，下载自己操作系统的安装包直接安装就可以了:

* window选择,msi安装包，Mac选择.pkg安装包，Linux会在后续部署中讲解
* 安装过程中会配置环境变量(让我们可以在命令行使用)
* 并且会安装**npm(Node Package Manager)-节点包管理**工具;

# 二、Node的版本工具(了解)
在实际开发学习中，我们只需要使用一个Node版本来开发或者学习即可。

但是，如果你希望通过可以快速更新或切换多个版本时，可以借助于一些工具:

* nvm:Node Version Manager;
* n:Interactively Manage Your Node.js Versions(交互式管理你的Node.js版本)

**问题:这两个工具都不支持window**

* n:nis not supported natively on Windows.
* nvm:nvm does not support Windows

Window的同学怎么办?

* 针对nvm，在GitHub上有提供对应的window版本:https://github.com/coreybutler/nvm-windows
* 通过 nvm install latest 安装最新的node版本
* 通过 nvm list 展示目前安装的所有版本
* 通过 nvm use 切换版本

# 三、版本管理工具：n

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743684974000ky1aml.png)




