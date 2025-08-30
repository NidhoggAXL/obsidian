# 一、Git rebase用法

在 Git 中整合来自不同分支的修改主要有两种方法：merge 以及 rebase。

**meige**：在master分支中`git merge experiment`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451558820000rknfd.png)


**rabase**：在experiment分支中`git rebase master`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745155910000goujtg.png)

什么是rebase呢？ 

* 在上面的图例中，你可以提取在 C4 中引入的补丁和修改，然后在 C3 的基础上应用一次； 
* 在 Git 中，这种操作就叫做 **变基（rebase）**； 
* 你可以使用 rebase 命令将提交到**某一分支上的所有修改**都移至另一分支上，就好像“**重新播放**”一样；

# 二、rebase的原理

rebase是如何工作的呢？ 

* 它的原理是首先找到这两个分支（即当前分支 experiment、变基操作的目标基底分支 master） 的最近共同祖先 C2； 
* 然后对比当前分支相对于该祖先的历次提交，提取相应的修改并存为临时文件； 
* 然后将当前分支指向目标基底 C3； 
* 最后以此将之前另存为临时文件的修改依序应用；

可以再次执行master上的合并操作：

```bash
git checkout master
git merge experiment
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17451560880005m1jq6.png)





