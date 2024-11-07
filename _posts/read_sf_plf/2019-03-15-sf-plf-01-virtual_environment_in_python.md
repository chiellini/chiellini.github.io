---
title: "Python 虚拟环境的使用和配置"
subtitle: "Python programming basic"
layout: post
author: "lizelin"
header-style: text
hidden: true
tags:
  - Programming
  - Blog/diary
---
### 本文主要介绍关于Python的虚拟环境virtualenv的使用以及如何进行项目迁移

---

### virtualenv 是一个创建隔绝的Python环境的工具。virtualenv创建一个包含所有必要的Python可执行文件的文件夹，用来管理Python工程所需的包。在一般情况下的时候，你的Python项目所使用的包和库函数都是全局的，是和你的全局环境的Python环境绑在一起的。比如常用的依赖包Numpy,是需要手动安装的。这导致你的项目进行迁移或者部署的时候非常不方便；当然你也不可能把所有可能用到的包都安装上，这样对于服务器来说负担也太大了。这就产生了virtualenv这个工具。使用这个工具可以对特定的项目安装特定的依赖包，并生成该项目必须的依赖环境，方便迁移。 

---

* WINDOWS

  * 使用cmd控制台。使用powershell和gitbash的均不能激活虚拟环境。
    * 在cmd中   dir命令等于ls，可以使用ctrl+c和ctrl+v进行粘贴复制 
  * 执行命令pip install virtualenv 在你的电脑上安装这个插件
  * 到你想要的位置，执行命令 virtualenv
    * ![1536564418367](
      https://github.com/chiellini/pictures_sources/blob/master/teach/Python/1536564418367.png?raw=true
  )
    * 出现以上结果，说明虚拟环境创建成功
  * 进入你的虚拟环境 cd teach/Scripts
  * 进入之后执行 activate
    * ![1536564678827](https://github.com/chiellini/pictures_sources/blob/master/teach/Python/1536564678827.png?raw=true)
    * ![153656486548](https://github.com/chiellini/pictures_sources/blob/master/teach/Python/234124124124.png?raw=true)
    * 出现以上结果说明成功进入你的虚拟环境
  * 随后在该cmd跳转到你的项目文件，执行你的项目，一般会报错。这是因为在这个虚拟环境下没有你需要的依赖包。你只需在该cmd下执行pip install <你需要的包> 即可安装到这个虚拟环境下。把所有需要的包安装之后，你的项目就能够在该cmd执行你的Python程序，并且都是最基本的包，没有多余的。可以利用pip list进行查看导入了什么包。
  * 可以执行之后，把你的依赖包写入requirements.txt，执行命令:pip freeze > requirements.txt 
  * 打开requirements.txt ，也可以查看你的依赖包。
    * 如果确实你的依赖包，请检查。
    * 如果是导出少了，可以手动添加，否则不要手动添加未使用的包，以免增添累赘。
  * 停用命令deactivate

---
* Linux环境

  * 安装

    ```
    pip install virtualenv
    ```

  * 基本使用

    * 为一个工程创建一个虚拟环境：

    ```
    $ cd my_project_dir
    $ virtualenv venv　　#venv为虚拟环境目录名，目录名自定义
    ```
    * 要开始使用虚拟环境，其需要被激活：

    ```
    $ source venv/bin/activate
    ```

* 随后在该终端跳转到你的项目文件，执行你的项目，一般会报错。这是因为在这个虚拟环境下没有你需要的依赖包。你只需在该终端下执行pip install <你需要的包> 即可安装到这个虚拟环境下。把所有需要的包安装之后，你的项目就能够在该终端执行你的Python程序，并且都是最基本的包，没有多余的。可以利用pip list进行查看导入了什么包。

* 可以执行之后，把你的依赖包写入requirements.txt，执行命令:pip freeze > requirements.txt 

* 打开requirements.txt ，也可以查看你的依赖包。

  - 如果确实你的依赖包，请检查。
  - 如果是导出少了，可以手动添加，否则不要手动添加未使用的包，以免增添累赘。

* 停用命令deactivate

---

完成上述工作之后，当你需要把你的项目或者别人的项目迁移的时候，这个项目所依赖的包就在requirements.txt里面了。

项目拷贝过来之后，创建你的本地的Python虚拟环境，并成功进入之后，变换目录到requirements.txt的位置，执行命令

```
pip install -r requirements.txt
```

该虚拟环境该项目所需要的包，不会对你本机的Python环境造成任何影响。