# 一、为什么会推荐使用pnpm？
**自我理解：**

在早期的使用 npm、yarn、cnpm 的时候存在一个最大的问题，在我们在电脑上面开发项目的时候，每一个项目都要对所使用的库进行一个下载。

虽然有缓存存在，但是缓存只是保存到缓存里面，当我们项目中使用的时候还是要下载解压到项目中。

如果项目很多的话，每一个项目下载相同的库就会造成电脑磁盘空间的肿大，同一个库下载了多份。

![[pnpm出现前的疼点|600]]

# 二、什么是pnpm呢？
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744184802000ngrbnd.png)


# 三、硬链接和软连接的概念
硬链接（hard link）： 

* 硬链接（英语：hard link）是电脑文件系统中的多个文件平等地共享同一个文件存储单元； 
* 删除一个文件名字后，还可以用其它名字继续访问该文件； 

符号链接（软链接soft link、Symbolic link）： 

* 符号链接（软链接、Symbolic link）是一类特殊的文件； 
* 其包含有一条以绝对路径或者相对路径的形式指向其它文件或者目录的引用；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744186125000rpouyb.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744186133000fnu5da.png)

在 VS Coder 中有小箭头的就表示软连接：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744189184000nx1w5n.png)


# 四、硬链接和软连接的演练
**文件的拷贝：** 文件的拷贝每个人都非常熟悉，会在硬盘中复制出来一份新的文件数据；

```
window: copy 原文件 拷贝文件
macos: cp 原文件 拷贝文件
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744187043000vw6ghy.png)

**文件的硬链接：**

```
window: mklink /H 拷贝文件 原文件 
macos: ln 原文件 拷贝文件
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744187112000i5qtyv.png)

**文件的软连接：**

```
window: mklink 拷贝文件 原文件 
macos: ln -s 原文件 拷贝文件
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744187148000tmte9p.png)

# 五、pnpm到底做了什么呢？
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744187643000a6v6a3.png)



# 六、pnpm创建非扁平的 node_modules 目录
当使用 npm 或 Yarn classic 安装依赖包时，所有软件包都将被提升到 node_modules 的 根目录下。

* 其结果是，源码可以访问 **本不属于当前项目所设定的依赖包**;

> 就是说我是通过 工具包 安装了 webpack ，但是因为 webpack 依赖一些包，在下载 webpack 的时候就会把依赖的包同时下载出来，
> 原本应该是放到 webpack 的 node_modules 文件里面的，但是 npm 、yarn……会进行 **扁平** 话处理，
> 把**依赖的包提升到和 webpack 同等级的目录**，这样在使用 `require("")`的时候就可以导入依赖包并进行使用。为什么可以查找到，查看[[03 require函数解析]]

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744197058000zp696k.png)


# 七、pnpm 的安装和使用

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17441974700007nuqz7.png)


# 八、pnpm的存储store
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744198611000t5sqgn.png)


同时在 Window 在 C 盘和 文件所在的盘都有一份硬链接数据。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744198507000g93cid.png)


