# 一、创建tag

对于重大的版本我们常常会打上一个标签，以表示它的重要性： 

* Git 可以给仓库历史中的某一个提交打上标签； 
* 比较有代表性的是人们会使用这个功能来标记发布[[02 package 配 置 文 件#四、依赖版本管理|结点]]（ v1.0 、 v2.0 等等）； 

创建标签： 

* Git 支持两种标签：轻量标签（lightweight）与附注标签（annotated）； 
* 附注标签：通过-a选项，并且通过-m添加额外信息；

```bash
git tag 版本号
git tag -a 版本号 -m "版本说明"
```

> [!warning] 创建标签的操作一定是在 git commit 之后，git push 之前的。

标签的查看：

```bash
git tag
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174506032200039x9th.png)


默认情况下，git push 命令并不会传送标签到远程仓库服务器上。 

* 在创建完标签后你**必须显式地推送标签到共享服务器上**，当其他人从仓库中克隆或拉取，他们也能得到你的那些标签；

```bash
git push origin 版本号 //当前版本号
git push origin --tags //所有版本号
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17450604220004k7zsc.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745060439000ax2fnx.png)

# 二、删除和检出tag

删除本地tag： 要删除掉你本地仓库上的标签，可以使用命令 `git tag -d 版本号标签`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745060508000xdo7jr.png)

删除远程tag： 要删除远程的tag我们可以通过`git push 远程仓库名 –-delete 版本号标签`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745060602000hgve39.png)


