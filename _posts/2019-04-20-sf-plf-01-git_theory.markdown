---
title: "Git 基础"
subtitle: "useful git basic theary which can help you version control in terminal"
layout: post
author: "lizelin"
header-style: text
catalog: true
tags:
  - 软件基础
  - Version Control
  - 笔记
---
#Git 基础
##1. Git 简史
同生活中的许多伟大事物一样，Git 诞生于一个极富纷争大举创新的年代。

Linux 内核开源项目有着为数众广的参与者。 绝大多数的 Linux 内核维护工作都花在了提交补丁和保存归档的繁琐事务上（1991－2002年间）。 到 2002 年，整个项目组开始启用一个专有的分布式版本控制系统 BitKeeper 来管理和维护代码。

到了 2005 年，开发 BitKeeper 的商业公司同 Linux 内核开源社区的合作关系结束，他们收回了 Linux 内核社区免费使用 BitKeeper 的权力。 这就迫使 Linux 开源社区（特别是 Linux 的缔造者 Linus Torvalds）基于使用 BitKeeper 时的经验教训，开发出自己的版本系统。 他们对新的系统制订了若干目标：

速度
简单的设计
对非线性开发模式的强力支持（允许成千上万个并行开发的分支）
完全分布式
有能力高效管理类似 Linux 内核一样的超大规模项目（速度和数据量）
自诞生于 2005 年以来，Git 日臻成熟完善，在高度易用的同时，仍然保留着初期设定的目标。 它的速度飞快，极其适合管理大项目，有着令人难以置信的非线性分支管理系统。

##2. 主要概念
###2.1 仓库
存放代码的目录，分为本地仓库和远程仓库，本地和远程可以通过 git remote add 建立关联。

本地仓库有三大分区：

**工作区 (Working Directory):** 是我们编辑代码的地方
**暂存区 (Stage or Index):** 数据暂时存放的区域，可以在工作区和版本库之间进行数据的交流
**版本库 (Commit History):** 存放已经提交的数据，push 的时候就是把这个区域的数据推送到远程仓库
###2.2 分支
git 中的分支本质上是一个指向某个 commit 的指针。


###2.3 文件的生命周
对于 git 仓库里的每一个文件（除了 .git 目录和被 .gitignore 忽略的文件），有如下几种状态：

Untracked 未跟踪
Unmodified 未修改
Modified 已修改
Staged 暂存区

​

##3. 常用操作
```
git init # 在当前目录下初始化一个本地 git 仓库
git status # 检查当前文件状态
git diff # 比较工作区和暂存区
git diff HEAD # 比较工作区和版本库
git diff --cached # 比较暂存区和版本库
git add <filename> # 将 <filename> 添加到暂存区
git add -A # 将所有文件添加到暂存区
git add . # 将当前目录下的所有文件添加到暂存区
git commit # 提交更改（将暂存区的文件提交到 Commit History）
git commit --amend # 修改 commit 信息
git push origin <branch> # 将本地分支推送到远程仓库
git pull origin <branch> # 将远程仓库的分支拉取到本地
git clone <repository> [<directory>] # 克隆远程分支到本地，repository 可以由 schema 为 http[s], ssh, git, ftp[s], file 等各种 uri 表示，也可以是 scp 风格的路径表示。directory 表示克隆下来的仓库目录名
git config [--global|--local] user.name "<username>" # 设置用户名，用户名会出现在 commit 信息里，加了--local参数只影响当前仓库的配置，加--global参数会影响本机上所有仓库的配置，默认是--local
git config [--global|--local] user.email "<email>" # 设置用户邮箱，邮箱会出现在 commit 信息里
git remote add origin <repository> # 添加一个远程分支，命名为 origin
git log [--oneline] # 查看 commit 信息
git log --oneline --graph # 查看 commit 节点树
```
##4. 高级操作
```
git branch # 查看本地分支
git branch -a # 查看所有分支，包括远程分支
git branch <name> # 创建一个和当前分支版本库一样的分支
git checkout <branch> # 切换分支
git checkout -b <branch> <start_point> # 创建一个新分支并切换，新分支的 HEAD 指针指向 start_point, start_point 可以是本地分支或远程分支的任意一个 commit
git reset --soft <commit> # 将版本库的 HEAD 指向 commit
git reset --mixed <commit> # 将版本库和暂存区的 HEAD 指向 commit
git reset --hard <commit> # 将版本库、暂存区和工作区的 HEAD 指向 commit，但不会影响为跟踪的文件
git rebase <branch> # 把当前分支变基到 branch 上
git stash # 将暂存区中的文件储藏起来
git stash apply # 恢复储藏的文件到暂存区
git revert <commit> # 撤销之前的某一个 commit
```
##5. 冲突解决
当发生冲突的时候，冲突的文件中会出现以下格式的内容。

解决冲突的时候，可以选择保留当前修改，保留另一个分支的修改，或是两个都不保留，重新编辑。

解决冲突的时候既要解决文本冲突，也要注意逻辑冲突。当冲突解决完成后，应该将当前文件加入暂存区，并执行对应命令加上 --continue 参数。
```
<<<<<<< HEAD
            modification belongs to current branch
=======
            modification belongs to other branch
>>>>>>> commit 38a1cab...
```
##6. .gitignore
文件 .gitignore 的格式规范如下：

所有空行或者以 ＃ 开头的行都会被 Git 忽略。
可以使用标准的 glob 模式匹配。
匹配模式可以以（/）开头防止递归。
匹配模式可以以（/）结尾指定目录。
要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。
```
# no .a files
*.a
```
```
# but do track lib.a, even though you're ignoring .a files above
!lib.a
```
```
# only ignore the TODO file in the current directory, not subdir/TODO
/TODO
```
```
# ignore all files in the build/ directory
build/
```
```
# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt
```
```
# ignore all .pdf files in the doc/ directory
doc/**/*.pdf
```
##7. Merge & Rebase
Merge: 合并两个分支

Rebase: 改变分支的 base commit

这两种操作都可以合并分支，rebase 的优势在于可以使 commit history 的线性程度更高。线性程度高的好处在于，浏览历史的时候更整洁，不容易碰到分叉，分叉部分的代码差异可能更大。
```
git merge <branch> # 把 branch 合并到当前分支
git rebase <commit> # 把当前分支 rebase 到 commit 上
```
这两种操作解释起来可以单独写一篇博客了，运行下面的练习，体会以下不同。
```
#!/bin/bash

commit() {
  touch $1 && git add $1 && git commit -m "$1"
}

git init

commit a
commit b
git checkout -b feat
commit c
commit d
git checkout master
commit e
commit f
commit g
git merge feat "Merge branch feat"

git log --oneline --graph

commit h
git checkout -b feat2
commit i
commit j
git checkout master
commit k
commit l
git rebase feat2

git log --oneline --graph
```
将上面的代码保存为 practice.sh 文件，运行练习
```
chmod +x practice.sh
./practice.sh
```
rebase黄金准则

永远不要 rebase 到一个共享的分支，只能 rebase 自己使用的私有分支。

##8. License
本作品采用知识共享 署名-非商业性使用-相同方式共享 2.5 中国大陆 许可协议进行许可。要查看该许可协议，可访问 http://creativecommons.org/licenses/by-nc-sa/2.5/cn/ 或者写信到 Creative Commons, PO Box 1866, Mountain View, CA 94042, USA。