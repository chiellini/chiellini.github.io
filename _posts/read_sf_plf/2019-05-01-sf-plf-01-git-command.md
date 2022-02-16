---
title: "Git 常用命令"
subtitle: "useful git command which can help you version control in terminal"
layout: post
author: "lizelin"
header-style: text
hidden: true
tags:
  - 软件基础
  - Version Control
  - 笔记
---

## 为什么你的 Git 仓库变得如此臃肿

git因commit的记录太大导致push失败解决方法


https://www.jianshu.com/p/7231b509c279

https://stackoverflow.com/questions/32715034/removing-files-from-git-history-bad-revision-error


**以下内容在git GUI都有，但是每次换一个环境要装ＧＵＩ也不现实，所以还是习惯用命令行吧**

参考<https://www.git-scm.com/book/zh/v2>

使用前配置

* git config --global user.name "chiellini"

* git config --global user.email "18319277690@163.com"

设置默认记住密码

* git config --global credential.helper store

检查状态

* git status
* git diff
* git diff --staged 查看已经暂存的

查看历史和版本

* git log
* git log -p -2 最近两个版本
* git log --stat　简要列出每次提交修改的文件

可以补充commit

```
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

并和远处同步

* git reset --hard origin/develop

取消本地修改

* git checkout .

查看所有分支

* git branch -a
* git checkout -b 本地分支名字　上面获得的远程分支全名

合并

* git merge your_tmp_branch

冲突

在不同分支中，对同一个文件的同一个部分进行了不同的修改，ｇｉｔ就没法干净的合并他们会报错

```
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

打开没有合并的文件，像下面

```
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
 please contact us at support@github.com
</div>
>>>>>>> iss53:index.html
```

现在就修改，选择你要的那部分就可以
选择完之后
git add <>
git commit
git push



只在一条分支上做开发，然后又冲突了的，某一方保存自己的修改文件，直接回退到远程版本（或者新建分支再参考上述合并）

git reset --hard origin

# .gitignore

忽略二进制或者无用文件.gitignore在git根目录下

使得ignore生效必须先清空git缓存器中具体命令如下

危险命令！谨慎使用！
* git rm -r --cached . 

* git add .
* git commit -m "update .gitignore"

看一个例子就明白了

```
我们再看一个 .gitignore 文件的例子：

# no .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in the build/ directory
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory
doc/**/*.pdf
```