## 简述
经过又一段时间的查阅文章,真是断断续续搞了n久,不过终于将驱动这块搞定了,妈妈再也不用担心我的Debian黑屏了.
<!-- more -->
## 预备知识

###关于单显卡和双显卡

- 笔记本**双**显卡：指笔记本拥有一个独立显卡和一个cpu集成的核心显卡，两个显卡可以通过系统切换使用，一般使用核心显卡相对节能，适合办公上网等。使用独立显卡性能较高，适合游戏和作图。
- 笔记本**单**显卡：指笔记本只有一个独立显卡，或只有一个主板板载集成显卡，或只有一个cpu集成的核心显卡。不能进行显卡切换。

###关于 nouveau 和 nvidia驱动

- nouveau：是一个自由及开放源代码显卡驱动程序，是为Nvidia的显示卡所编写，此驱动程序是由一群独立的软件工程师所编写，Nvidia的员工也提供了少许帮助。简而言之就是开源驱动。
- nvidia驱动：通常是指有NVIDIA官方提供的NVIDIA显卡驱动。

### 目前linux下有三种optimus的实现
1. nouveau-only: PRIME GPU offloading using nouveau
2. nvidia-only: nvidia's more recent implementation, also packaged as nvidia-prime in Ubuntu
3. nouveau or nvidia: bumblebee

## 新手误解
1. 我是否需要为我的笔记本/台式机安装Nvidia驱动？
	> 如果是双显卡，不是用Debian作图形，游戏等工作，实际上是不需要安装Nvidia的驱动的。
2. 关于对NvidiaGraphicsDrivers Wiki的误解。
	> 这个wiki是讲解怎么安装Nvidia的驱动的（单显卡中的一种），并不是双显卡。
3. 是不是Debian已经自动安装好了Nvidia开源驱动（nouveau）呢?
	> 执行lspci \-v 就能看到了。
	> 例如看到这样的就说明Debian已经为你安装了开源的nouveau驱动。
	> Kernel driver in use: nouveau
	> Kernel modules: nouveau

## 黑屏解决方案(写在前面)
大兄弟,如果你已经黑屏了，那么ctrl+alt+F1进入终端，然后使用root身份登陆,然后执行下面的代码.(sudo 是为普通用户准备的)
> sudo apt-get purge nvidia*
sudo rm /etc/X11/xorg.conf

## 双显卡切换的解决方案
### Bumblebee简述
Bumblebee旨在为NVIDIA Optimus笔记本电脑提供GNU / Linux发行版的支持。使用Bumblebee，您可以使用NVIDIA卡渲染,使用Intel卡显示图形。

Bumblebee，开机加载的是intel的驱动，程序默认也都是用intel的集显，如果需要用独显要用optirun运行程序，这样能做到最大程度的提高电池续航能力。

### 安装bumblebee
其实很简单，[see it](https://wiki.debian.org/Bumblebee#Power_Management)
添加32位支持（如果是64位系统的话）
> sudo dpkg –add-architecture i386

个人怀疑一部分安装完后黑屏的情况可能和没有执行这一步有关。

更新源,安装bumblebee

> sudo apt-get update
sudo apt-get install bumblebee-nvidia primus primus-libs:i386


### 使用bumblebee
要在终端中运行离散NVIDIA卡运行应用程序：
> $ optirun [options] <application> [application-parameters]

例：
> $ optirun glxgears -info

有关optirun的选项列表，请使用man optirun打开联机帮助页或运行：
> $ optirun --help

### 在Steam中使用bumblebee
1. 从Steam客户端的“库”页面中选择要使用Nvidia显卡运行的游戏，右键单击并选择“属性”。
2. 单击设置启动选项按钮，并为命令行指定primusrun ％command％。
3. 保存您的更改。此方法允许您选择在每个游戏基础上使用离散NVidia GPU。
