# 一、Git的远程分支
远程分支是也是一种分支结构： 

* 以 `<remote>/<branch>` 的形式命名的； 

如果我们刚刚clone下来代码，分支的结构如下： 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451480010009r2yoe.png)

如果其他人修改了代码，那么远程分支结构如下： 

* 你需要通过fetch来获取最新的远程分支提交信息；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451480760008rp6ub.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451480810003u8j45.png)


# 二、远程分支的管理
**操作一：推送分支到远程** 

* 当你想要公开分享一个分支时，需要将其推送到有写入权限的远程仓库上；
* 运行 git push ；

```
git push origin <branch>
```

* 首先创建本地分支并进入分支：![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745152909000m9jesa.png)
* 然后让本地develop分支追踪上游的develop分支：![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745153008000kb2zvh.png)
* 推送到远程仓库，这样上游分支就会设置为远程的一个分支，本地和远程的分支建立联系。![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745153149000ajhmwd.png)![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745153241000gdw92g.png)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451532230008qlrpg.png)

main分支并没有进行改变：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745153279000r5v654.png)


**操作二：跟踪远程分支** 

* 当**克隆一个仓库时**，它通常会自动地创建一个跟踪 origin/master 的 master 分支(**github为main分支**)； 
* 如果你愿意的话可以设置其他的跟踪分支，可以通过运行 `git checkout --track <remote>/<branch>`
* 如果你尝试检出（checkout）的分支 (a) 不存在且 (b) 刚好只有一个名字与之匹配的远程分支，那么 Git 就会为你创建一个跟踪分支；

```
git checkout --track <remote>/<branch> 
git checkout
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174515416900083bg1j.png)


**操作三：删除远程分支** 

* 如果某一个远程分支不再使用，我们想要删除掉，可以运行带有 `--delete` 选项的 git push 命令来删除一个远程分支。

```
git push origin --delete <branch>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745154256000aq97zl.png)

github 远程上面就没有了 develop 分支的指针：![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745154286000e7y4cn.png)


