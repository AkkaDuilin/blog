---
title: Git
categories:
  - Git
  - Github
  - null
tags:
  - Git
  - null
copyright: true
date: 2022-08-29 11:27:33
permalink:
description:
image:
---

<img src="https://" alt="" style="width:100%" />  

**前言**

Git/Github 相关学习笔记

git协同开发流程

参考博客：
https://www.jiyik.com/w/git

https://www.cnblogs.com/failymao/p/14929004.html#step-3%E6%8A%8A%E8%87%AA%E5%B7%B1%E5%BC%80%E5%8F%91%E8%80%85%E4%BB%93%E5%BA%93clone%E5%88%B0%E6%9C%AC%E5%9C%B0


<!-- more -->

# 仓库操作

一个Git仓库是项目的一个虚拟存储。它允许您保存代码的版本，可以在需要时访问这些版本。

Git 有一个额外的保存机制，称为“ stash ”。stash 是一个临时存储区域，用于存储尚未准备好提交的更改。
| 序号 | 方法 | 方法 |
| ---- | ---- | ---- |
| 1    |   git init   |  创建新仓库    |
| 2    |  git clone    |  创建仓库副本 --branch 克隆特定标签    |
| 3    |    git add    |  将修改添加到暂存区  可以是文件和文件夹    |
| 4    |  git commit      | 将暂存提交到项目历史记录 -am 立即创建所有暂存更改的提交并附加提交消息     |
| 5    |  git stash    |   暂时搁置（或隐藏）对工作副本所做的更改    |
| 6    |  git diff    |    比较更改    |
| 7    | git status     |   显示工作目录和暂存区的状态   |
| 8    |  git log      |  显示已提交的快照的所有的历史信息    |
| 9     | git tag       |   标签 -a 添加注释 -m -f更新 -d删除    |


# 撤销更改

先使用 git log --oneline 查看修订的ID

1. 
使用 git checkout ID  查看此ID的提交 检出特定的提交将使仓库处于“分离 HEAD ”状态

从分离的HEAD 状态，我们可以执行git checkout -b new_branch_jiyik 命令。 这将创建一个名为 new_branch_jiyik 的新分支并切换到该状态。

2. 
git revert HEAD

撤消对仓库提交历史的更改

创建一个与上次提交相反的新提交

3. 
git reset


4.  https://blog.csdn.net/weixin_44137575/article/details/108142088
git clean 清理仓库

git clean 从你的工作目录中删除所有没有 tracked，没有被管理过的文件。

n ：显示将要被删除的文件

d ：删除未被添加到 git 路径中的文件（将 .gitignore 文件标记的文件全部删除）

f ：强制运行

x ：删除没有被 track 的文件


# 远程仓库

```
git remote
git remote 命令本质上是一个接口，用于管理存储在仓库的 ./.git/config 文件中的远程条目列表。

git fetch <remote>
从仓库中获取所有分支。 这还会从其他仓库下载所有必需的提交和文件。

git fetch <remote><branch>
与上面的命令相同，但仅获取指定的分支。

git fetch --all
获取所有已注册远程分支

git fetch --dry-run
--dry-run 选项将执行命令的演示运行。 它将输出在获取期间将采取的操作示例，但不应用它们。


git push <remote> <branch>
将指定的分支以及所有必要的提交和内部对象推送到远程仓库的分支 。 这会在目标仓库中创建一个本地分支。 为了防止你覆盖提交，当发现推送的分支的提交不是最新的提交，也就是慢于远程分支的提交时，Git 不会让你推送。

git push <remote> --force
该命令上面的命令相同，但是它是强制推送，即使当前要推送的分支的提交慢于远程仓库的提交版本。除非你绝对确定自己知道自己在做什么，否则不要使用 --force 选项。

git push <remote> --all
将所有的本地分支推送到远程。

git push <remote> --tags
当推送分支或者使用 --all 选项时，Git 并不会对本地的标签（tag）进行推送。如果要将本地的标签推送的远程仓库，则需要--tags 选项。


git pull <remote>
获取当前分支的指定远程分支并立即将其合并到本地分支中。 这与 git fetch <remote> 后再执行 git merge origin/<current-branch> 相同。

git pull --no-commit <remote>
与默认调用类似，获取远程内容但不创建新的合并提交。

git pull --rebase <remote>
与上一个 pull 相同，单不是使用 git merge 将远程分支与本地分支合并，而是使用 git rebase。

git pull --verbose
显示在拉取期间的下载的内容和合并的详细信息。
```
# 分支

git中，分支操作则是每个开发人员日常工作流。
每个开发者的仓库都有自己的分支路线，而这些分支路线会通过代码汇总映射到源仓库中去。

分为
1. 永久性分支
master branch：主分支
develop branch：开发分支 每个开发者的仓库相当于源仓库的一个镜像
开发者把功能做好以后，是存放到自己的develop中，当测试完以后，可以向管理者发起一个pull request，请求把自己仓库的develop分支合并到源仓库的develop中。

2. 临时性分支
feature branch：功能分支 用于开发项目的功能的分支 该分支上进行功能的开发，开发完成以后再合并到develop分支上 命名一般为feature-*
release branch：预发布分支
hotfix branch：bug修复分支

## git branch 常见选项

```
1. git branch
或者
git branch --list
列出仓库中的所有分支。

2. git branch <branch>
创建一个名为<branch>的新分支。这并没有检出新的分支。

3. git branch -d <branch>
删除指定的分支。这是一个“安全”操作，因为 Git 会阻止我们删除具有未合并更改的分支。

4. git branch -D <branch>
强制删除指定的分支，即使它有未合并的更改。如果想永久丢弃与特定开发线相关的所有提交，则可以使用此命令。

5. git branch -m <branch>
将当前分支重命名为<branch>。

6. git branch -a
列出所有远程分支。
```
## git checkout 

git checkout 在分支上使用时会改变 HEAD 引用的目标。 它可用于创建分支、切换分支和检出远程分支。

```
1. 切换分支 git checkout branch_id

2. 创建分支并切换 git checkout -b <new-branch>
```

## git merge
将多个提交序列合并为一个统一的历史记录

https://www.jiyik.com/w/git/git-merge


# git协同开发

https://developer.aliyun.com/article/604633

# 
# MORE

<hr />
版权信息