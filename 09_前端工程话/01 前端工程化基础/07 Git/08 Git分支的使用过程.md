# 一、git和commit的本质

几乎所有的版本控制系统都以某种形式支持分支。 

* 使用分支意味着你可以把你的工作从开发主线上分离开来，以免影响开发主线。

在进行**提交操作时**，Git 会保存一个**提交对象**（commit object）： 

* 该提交对象会包含一个指向**暂存内容**快照的指针； 
* 该提交对象还包含了作者的姓名和邮箱、提交时输入的信息以及**指向它的父对象的指针**； 
	* 首次提交产生的提交对象**没有父对象**，普通提交操作产生的提交对象有一个父对象； 
	* 而由多个分支合并产生的提交对象有多个父对象；


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174513072700001kk8g.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745130749000qpmslz.png)


1. 当创建一个 git 仓库的时候，`git init`初始化：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745131181000ic567o.png)

看 objects 里面存放的东西

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745131108000k72l32.png)

2. 进行`git add .`操作：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451312480006d8o93.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745131433000o3u0gd.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745131712000lcx3pi.png)


会多出两个文件夹，并且文件夹里面存放的东西是二进制的格式，要查看里面的内容需要使用 `git cat-file -t` 查看文件格式（这个命令默认查看的就是 objects 里面的文件）。

```bash
git cat-file -t objects中文件的文件夹名+文件名（可以省略后面多位）
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451314120003xu63y.png)

blob 说明是一个二进制文件，如果要查看内容的话就是是用`git cat-file -p`命令，也可以对文件名进行省略

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745131731000rsfkse.png)

> 可以看到这里面存放就是创建的两个文件内容，这样可以得出，**git的本质是把文件与内容保存到 objects 里面。**

 3. 那么git commit 操作会是什么样子呢？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745131898000qsax0e.png)

会多出两个文件：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451319500002c3t77.png)

那么这两个文件夹里面放的又是什么呢？使用`git cat-file -p`命令来看看回事什么。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745132030000nvp3yv.png)

可以看出这两个文件，一个文件是存放着文件的索引，另一个是存放着提交的信息。

提交信息中有一个 tree 这个又是什么呢？这个就是提交的另外一个存放打印内容的文件（362f）。

而 git 是如何找到本次提交的呢？`git log`查看一下提交的时候 commi id 是什么

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745132520000jgtls4.png)

**会发现提交时的校验和（commit id）就是 2348 ，存放着两个打印文件索引的文件。**

# 二、git master分支

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745133774000scxiu9.png)

可以通过下面命令来查看处于那个分支(branch)：

```bash
git branch
```

# 三、Git创建分支

Git 是怎么创建新分支的呢？  很简单，它只是为你创建了一个可以移动的新的指针；

比如，创建一个 testing 分支， 你需要使用 git branch 命令：

```bash
git branch testing
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745133995000hqvh1v.png)

那么，Git 又是怎么知道当前在哪一个分支上呢？ 

* 也很简单，它有一个名为 HEAD 的特殊指针；
* HEAD指针所指的就是当前所处分支，以及所处的文件状态

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745133856000jc7dii.png)

切换指针使用命令(**本质是切换HEAD指针的指向**):

```bash
git checkout testing
```

> [!tip] 补充
> 
> git checkout 也可以通过标签（tag）进行切换`git checkout v1.0.0`,但是不能更改代码。（tag只是一个标记，更改要到一个工作流里面（分支））
> 
> 如果需要更改的话，那必须在切换后，创建一个分支，这样才可以进行修改代码。


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451339330000or5hw.png)

# 四、Git分支提交

如果我们指向某一个分支，并且在这个分支上提交：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451340700007w0f7q.png)

你也可以切换回到master分支，继续开发：

```bash
git checkout master
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745134127000r3wmak.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745134445000f51uda.png)

# 五、创建分支同时切换

创建新分支的同时切换过去 

* 通常我们会在创建一个新分支后立即切换过去； 
* 这可以用 `git checkout -b 新的分支名` 一条命令搞定；


# 六、为什么需要使用分支呢？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745137351000piuqc6.png)


# 七、分支开发和合并

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745137396000wdksrv.png)

来看一下流程：

1. 在 master 分支上开发到 c2 ，并在 c2 打上标签 tag v1.0.0

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745137780000wrhxeq.png)

2. 继续在 master 上面开发到 c4

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745137904000za56n8.png)

3. 回退到 tag： v1.0.0 版本，创建并切换到 hotfix 分支

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745138262000vixb5l.png)

> 也可以使用`git switch -c hotfix`来创建并切换分支

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745138736000owqhhe.png)


4. 在 hotfix 分支进行修复bug并打上标签 tag v1.0.1，最后提交。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745138893000z3deyy.png)

5. 切换回master分支

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745138975000ap1gxi.png)

6. 在 master 里面对 hotfix 分支和 master 分支进行合并

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745139076000upttjk.png)

> [!tip] 在进行合并的时候，这个时候代码内容回增加一些标识：
>* 第一种手动：通过手动更改来进行对代码的更改
>* 第二种自动：在 vs coder 中会智能的更改，可以在 vs coder 里面进行选择。

这里一般选择 **保留双方更改**：这样就会进行不同代码的合并

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174513930100033lnwk.png)

7. 对合并后的版本进行一个提交并查看分支情况

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745139644000yagdkx.png)

# 八、查看和删除分支

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745140536000qj3xtv.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745140668000luhuzh.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745140682000w29ca7.png)

> [!tip] 注意：
移除分支，只是删除指向当前分支的指针，或者说当前分支的名字，当前分支本身的内容并没有删除。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745140793000dr9cpp.png)

> hotfix 分支指针已经不存在。

