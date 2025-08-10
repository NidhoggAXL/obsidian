# 一、什么是远程仓库？
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17448924110001jyrw9.png)

**服务器和Git服务器的关系：**

* Git 服务器是搭建在 一台服务器 上面的，**并不是说有专门的一种服务器是Git服务器**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744892487000wkqk2w.png)


# 二、远程仓库的验证(gitee)
常见的远程仓库有哪些呢？目前比较流行使用的是三种： 

* GitHub：https://github.com/ 
* Gitee：https://gitee.com/
* 自己搭建Gitlab：自己搭建的网络地址

对于私有的仓库我们想要进行操作，远程仓库会对我们的身份进行验证： 

* 如果没有验证，任何人都可以随意操作仓库是一件非常危险的事情；

目前Git服务器验证手段主要有两种： 

* 方式一：基于**HTTP的凭证存储（Credential Storage）**； 
* 方式二：基于**SSH的密钥**；

## 2.1 凭证
因为本身HTTP协议是**无状态的连接**，所以每一个连接都需要用户名和密码： 

* 如果每次都这样操作，那么会非常麻烦； 
* 幸运的是，Git 拥有一个凭证系统来处理这个事情；

> [!tip] 什么是无状态链接？
比如我们访问网页的时候需要输入用户名和密码，HTTP是不会记录这些信息的，当再次发起网络请求的时候就需要再次输入用户名和密码。
>
**但是为什么有时候访问网页的时候不需要输出用户名和密码呢？**
这是我们浏览器中存放了我们访问过的cookie，再次访问的时候就会使用cookie，这样就不需要再次输入
>
**是 cookie 做了记录，并不是HTTP**

有一些 Git Crediential 的选项可以解决上面的问题： 

* 选项一：默认所有都不缓存。 每一次连接都会询问你的用户名和密码； 
* 选项二：“cache” 模式会将凭证存放在内存中一段时间。 密码永远不会被存储在磁盘中，并且在15分钟后从内存中清除； 
* 选项三：“store” 模式会将凭证用明文的形式存放在磁盘中，并且永不过期； 
* 选项四：如果你使用的是 Mac，Git 还有一种 “osxkeychain” 模式，它会将凭证缓存到你系统用户的钥匙串中（加密的）； 
* **选项五**：如果你使用的是 Windows，你可以安装一个叫做 “Git Credential Manager for Windows” 的辅助工具；
	* 可以在 https://github.com/Microsoft/Git-Credential-Manager-for-Windows 下载。
	* 安装 Git 的时候已经默认安装啦

在 git 命令行中输入`git conifg credential.helper`如果显示如下，就说明是安装了 Git Credential Manager for Windows

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174489745600000shjq.png)

这样就可以不用每次都要输入凭证啦

### 2.1.1 从远程仓库clone操作

复制登录的 HTTP 凭证

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17448982520002na8x1.png)

在 git bash 中输入命令进行 clone:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17448982990004p05bl.png)

进行用户名和密码的输入，就会从 gitee 中 clone 下载下来：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744898358000s0aeak.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17448983650005bd56p.png)

### 2.1.2 push到远程仓库
对 clone 的文件进行修改，并 `git commit -a -m "测试"`操作

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17448985400007n8xld.png)

方便后续在 gitee 中观察，改变 clone 文件的名字看看 push 到gitee 会有上面改变：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17448989560007jp7uu.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744898824000bfe0pu.png)

现在已经 push 到远程仓库(gitee)，我们刷新gitee就可以看到push后的文件：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17448988980002u33oa.png)

可以看到这个**总文件的名字**并没有发生改变：但是我们**子文件的内容是发生改变的。**

> 从上面也可以看出，是在文件里面操作的 git 操作，只会对 文件内的所有内容进行改变，并不会改变总文件夹的名字。

比如我们现在创建一个 index.html 本地文件，并把它 push 到远程仓库：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744899150000333dza.png)

现在本地仓库修改 index.html 在push到gitee，看会不会改变：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744899302000ccv0i3.png)

> 这样就可以明显的看出来，子文件的改变了。


## 2.2 删除凭证
在 window 控制面板中就可以删除凭证：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744899570000wihdzi.png)

## 2.3 SSH密钥
Secure Shell（安全外壳协议，简称SSH）是一种加密的网络传输协议，可在不安全的网络中为网络服务提供安全的传输环境。 

SSH以**非对称加密实现身份验证**。 

* 例如其中一种方法是使用自动生成的公钥-私钥对来简单地加密网络连接，随后使用密码认证进行登录； 
* 另一种方法是人工生成一对公钥和私钥，通过生成的密钥进行认证，这样就可以在不输入密码的情况下登录(**常见情况**)； 
* **公钥需要放在待访问的电脑（服务器）之中，而对应的私钥需要由用户自行保管**；

> [!tip] 公钥和私钥怎么进行验证的
> 当我们要 clone 远程git服务器的时候，git服务器里面存放了公钥，本地电脑存放私钥，这个时候就会那本地的私钥和远程服务器的公钥进行验证。

如果我们以SSH的方式访问Git仓库，那么就需要生产对应的公钥和私钥：

* 在 git bash 中进行产生，cmd中可能不支持这个命令

```
ssh-keygen -t ed25519 -C "your email"
或者
ssh-keygen -t rsa -b 2048 -C "your email"
```

* -t：后面是加密的方式
* -C： 后面是 自己的邮箱（**C要大写**）

### 2.3.1 生成SHH密钥
生成SHH的公钥和私钥

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744901103000i8lqhg.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744901163000aj7vzw.png)

### 2.3.2 添加公钥到服务器

讲公钥 （.pub）后缀的文件内容复制到gitee中的公钥设置里面：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17449013750003jjnde.png)

点击确定，输入密码后就添加成功公钥了

### 2.3.3 本地私钥进行clone
复制 SHH 的密钥进行 clone

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744901541000zn8qjp.png)

### 2.3.4 私钥进行push
后续的修改和 HTTP 相同的 push 操作相同

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17449017000001yedki.png)


# 三、管理远程服务器
查看远程地址：比如我们之前从Gitee上clone下来的代码，它就是有自己的远程仓库的：

```
git remote 
git remote –v 
-v是—verbose的缩写(冗长的)
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174495510500028x8ij.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744955119000hip052.png)

添加远程地址：我们也可以继续添加远程服务器（让本地的仓库和远程服务器仓库建立连接）：

```
git remote add
git remote add origin https://gitee.com/aoDraco/web-git-demo.git
```

> 远程仓库默认名为 origin

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744965482000quhgnl.png)

重命名远程地址： `git remote rename 旧名字 新名字`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744965595000qauf55.png)

移除远程地址： `git remote remove 名字`

到这里如果进行 **git pull** 会报错误，错误的原因如下：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744966659000wf3wth.png)

> There is no tracking information for the current branch.
> 当前分支机构没有跟踪信息。
> Please specify which branch you want to merge with.
> 请指明需要合并的分支

## 3.1 本地分支的上游分支(跟踪分支)
问题一:当前分支没有track的分支

原因:当前分支没有和远程的 origin/master 分支进行跟踪

* 在没有跟踪的情况下，我们直接执行pul操作的时候必须指定从哪一个远程仓库中的哪一个分支中获取内容;
* 前面已经更改了远程仓库在本地的名字，所以要使用 demo 而不是 origin。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17449668830000d148r.png)

如果我们想要直接执行 **git fetch** 是有一个前提的:**必须给当前分支设置一个跟踪分支:**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744967055000ymhff6.png)

## 3.2 拒绝合并不相干的历史
3.1 设置了分支，是否可以进行pull了呢？还是会有错误

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744967147000xd8ham.png)

**原因**:我们将两个不相干的分支进行了合并:

解释说明:https://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories-on-rebase

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744967442000w7ok84.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744967950000w1nhpi.png)

```
git merge --allow-unrelated-histories
```

>[!tip] 什么是没有必要的历史？
> git 服务器保存了一些历史的改变记录，当我们在本地创建项目的时候也会保存一些历史记录，这个时候要想和 git 服务器进行项目的合并，就会存在一些没有必要的历史。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744982443000vcfvge.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744982451000mx3r8r.png)

# 四、远程仓库的交互
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17449826920003oqp2r.png)

# 五、远程仓库总结
## 5.1 从远程仓库直接clone项目
```
git clone 远程仓库地址
git add .
git commit -m "提交信息"
git pull //是git fetch与git merge 的命令合并
git push //提交本地仓库信息到远程
```

## 5.2 开发一个全新项目

### 5.2.1 本地无项目
先创建一个远程的仓库，在从远程clone下来[[06 Git远程仓库和验证#五、远程仓库总结#5.1 从远程仓库直接clone项目|项目]]，在进行项目的搭建

### 5.2.2 本地有项目
#### 第一种方式

```
git remote add origin 远程仓库地址
git fetch
git branch --set-upstream-to=origin/master(github上面是main)
git merge --allow-unrelated-histories
git config push.default upstream
git push
```

git remoter add origin xxx：和远程仓库建立连接，这个时候只是建立了连接，当是**本地并不知道建立连接的远程仓库的分支是什么。**

git fetch：将远程仓库的内容下载到本地的 .git 文件（**并没有和本地文件进行合并**）



git branch --set-upstream-to=origin/master(**github上面是main**)：这是设置本地分支的上游分支是远程仓库的 origin/master(github上面是main) 分支（**让本质知道远程仓库的分支**）

* **这个操作之前，一定要进行`get fetch`操作，不然就会报如下的错误。**
* 如果不是就会报下面的错误：![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745148716000iqmzyi.png)
* 意思是：![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745148756000bqjdy3.png)

git merge --allow-unrelated-histories：就是对于不相关的历史进行合并

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451503570006zc2td.png)

git config push.default upstream：更改本地的配置文件，**使得 push 的默认为上游分支**

* 这个操作也可以不做，只是后面进行 push 操作的时候要选定push的位置例如`git push origin/master`

#### 第二种方式

```
git remote add origin 远程仓库地址
git fetch
git branch --set-upstream-to=origin/master(github上面是main)
git merge --allow-unrelated-histories
git checkout --track origin/main
git push
```

**当然还有一种更加方便的解决办法**：在本地创建一个跟踪远程分支的分支

```
git checkout --track origin/main
```

> 这样本地就会有一个 main 的分支是跟踪远程 main 分支了,这个时候就可以对 master 分支进行删除（也可以不删除）。![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451509870002zslh8.png)

如果要**删除本地的** master 分支，必须使用分支的[[08 Git分支的使用过程#八、查看和删除分支|强制删除]]

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745151206000zsm4k5.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451512620001m1xrn.png)

# 六、开源协议
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174498344400022rn7v.png)

MIT 是使用最多的（**最宽松**）


# 七、github的ssh和http错误
从github中进行clone操作，本地开启了代理报如下两个错误怎么解决：

2.  进行ssh的clone操作，错误是

>ssh: connect to host github.com port 22: Connection refused
>fatal: Could not read from remote repository.

>[!tip] 原因以及解决
> 原因就是![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17450582030008tmot7.png)
> 解决办法就是在![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745058361000zamfsl.png)


3.  进行https的clone操作，错误是
>fatal: unable to access 'https://github.com/NidhoggAXL/obsidian.git/': Failed to connect to github.com port 443 after 2087 ms: Could not connect to server

这个错误就是国内的一些运营商对访问做了一定的截取，也有解决的办法但是太过麻烦。


