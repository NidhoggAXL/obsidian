# 一、文件状态的划分

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744810402000ero294.png)

commit - 提交
Untracked - 未跟踪
modifi - 修改

# 二、Git操作流程图
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744810866000ui9g2b.png)

**index（索引）指的就是 staged（暂存、缓区）**

**working directory（工作区）就是编写代码的地方**

# 三、检测文件的状态
在有Git仓库的目录下新建一个文件，查看文件的状态：

```
git status
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17448128310003b5ml6.png)

Untracked files：未跟踪的文件 

* 未跟踪的文件意味着 Git 在之前的提交中没有这些文件； 
* Git 不会自动将之纳入跟踪范围，除非你明明白白地告诉它“我需要跟踪该文件”；

我们也可以查看更加简洁的状态信息：

```
git status -s
git status --short
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744812933000olxb8n.png)

> 左栏指明了暂存区的状态，右栏指明了工作区的状态；
> **? 表示没有处于那个状态**


# 四、文件添加到暂存区
跟踪新文件命令： 使用命令 git add 开始跟踪一个文件。

```
git add 跟踪的文件
```

跟踪修改的文件命令： 

* 如果我们已经跟踪了某一个文件，这个时候修改了文件也需要重新添加到暂存区中；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744813502000lo83s7.png)

通过git add . 将所有的文件添加到暂存区中：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744813514000xbr1se.png)

# 五、git忽略文件

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17448143850001lhv6u.png)

>[!tip] 前后端忽略文件区别
> 前端一般都是通过脚手架已经配置好的了
> 后端的话可以去 Github 上面搜索 gitignore ，会有 Github 总结好的一些关于各种编程的忽略文件
> 如果需要添加话，在进行自我的添加

# 六、文件更新提交
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744889639000lmx5hm.png)


# 七、git的校验和(了解)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744889960000nb1kkg.png)

校验和也会称之为 **commint id**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744890952000zpg3hm.png)


# 八、查看提交历史

在提交了若干更新，又或者克隆了某个项目之后，有时候我们想要查看一下所有的历史提交记录。

这个时候我们可以使用**git log命令**： 

* 不传入任何参数的默认情况下，git log 会按时间先后顺序列出所有的提交，最近的更新排在最上面； 
* 这个命令会列出每个提交的 SHA-1 校验和、作者的名字和电子邮件地址、提交时间以及提交说明；

```
git log
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744891464000ndnjbc.png)

```
git log --pretty=oneline
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744891498000586loj.png)

```
git log --pretty=oneline --graph
//graph-图
```

**这个命令主要是查看分支的情况的：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744891606000el51qa.png)

# 九、版本回退

如果想要进行版本回退，我们需要先知道目前处于哪一个版本：**Git通过HEAD指针记录当前版本。** 

* HEAD 是当前分支引用的指针，它总是指向该分支上的最后一次提交； 
* 理解 HEAD 的最简方式，就是将它看做 **该分支上的最后一次提交** 的快照；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744891673000w27ojb.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744891690000iwn93y.png)

我们可以通过HEAD来改变Git目前的版本指向： 

* 上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`； 
* 如果是上1000个版本，我们可以使用`HEAD~1000`； 
* 我们可以可以**指定某一个commit id**；
	* commit id 可以是前面几位数字（重复较少的时候）

```
git reset --hard HEAD^ 
git reset --hard HEAD~1000 
git reset --hard 2d44982
```

> HEAD 可以小写，但是一般都是大写
> hard - 硬




