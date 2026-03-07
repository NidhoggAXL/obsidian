# 一、获取Git仓库 

我们需要一个Git来管理源代码，那么我们本地也需要有一个Git仓库。 

通常有两种获取 Git 项目仓库的方式： 

* 方式一：**初始化一个Git仓库**，并且可以将当前项目的文件都添加到Git仓库中（目前很多的脚手架在创建项目时都会默认创建一个Git仓库）； 
* 方式二：从其它服务器 **克隆（clone） 一个已存在的 Git 仓库**（第一天到公司通常我们需要做这个操作）；

在初始化仓库的时候，我们希望是使用 git Bash 的命令标识行来进行命令的编写，因为会比 CMD 增加一些 git 的命令。
通过下载 Git 后有了 Git Bash，这个时候需要就可以在 VS Coder 中修改默认终端啦

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744807820000co20zf.png)


方式一：初始化Git仓库 

* 该命令将创建一个名为 .git 的子目录，这个子目录含有你初始化的 Git 仓库中所有的必须文件，这些文件是 Git 仓库的核心； 
* 但是，在这个时候，我们仅仅是做了一个初始化的操作，你的项目里的文件还没有被跟踪；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744809356000v00q54.png)

方式二：从Git远程仓库

```shell
git clone 仓库地址
```



