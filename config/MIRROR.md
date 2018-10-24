## 修改更新源

### Debian mirrors是什么

之前在介绍Debian的生命周期的时候,有提到Debian的stable, testing, unstable, experimental这些发行版本,然而这些发行版本的软件包都是在哪里保存的呢?就是主软件仓库,而这个主要的软件仓库因为全球网络访问而难以负载,为了减轻中央服务器的压力,全球数百个服务器通过同步主要软件仓库来减轻主要服务器的压力,而这些服务器上的软件仓库就被称之为Debian mirrors.

Debian mirrors可以分成主要与次要站。定义如下：

+ **主要镜像站**有足够的带宽，能每天 24 小时上线，有好记的名称如 ftp.<国家\>.debian.org.
这些镜像站会自动跟 Debian 档案库同步更新.

+ **次要镜像站**可能对于它们镜像的东西有所管制 (基于空间限制)。 身为一个次要镜像站并不代表它会比其他主要镜像站慢或是较少更新。

### 为什么要修改更新源

1. 用户可以使用Debian mirrors 网络安装Debian，从jigdo建立的CD，并为已安装的系统升级.
2. 通过修改距离自己比较近的安全的镜像源可以使得下载过程变得快速.
3. 使用自己熟悉的第三方源有益于安装配置官方源里没有的软件包.


### 如何修改更新源

Debian使用Deb软件包来管理软件。apt-get是Debian的Deb软件包管理工具，它的最底层是调用dpkg包管理程序来配置软件包，通过apt-get工具可使我们很好地解决软件包的依赖关系，方便软件的安装和升级。

要使用好apt-get就要配置sources.list的资源文件，资源文件指向Debian系统的软件仓库，apt-get会从该软件仓库下载安装各种软件包。sources.list文件位于/etc/apt目录下,另外使用 /etc/apt/sources.list.d/ 目录下的所有文件作为补充，二者的并集作为结果.
文件内容类似于下面所示：

> deb http://ftp.cn.debian.org/debian/ testing main contrib non-free
>deb-src http://ftp.cn.debian.org/debian/ testing main contrib non-free
>
> deb http://ftp.cn.debian.org/debian/ testing-updates main contrib non-free
> deb-src http://ftp.cn.debian.org/debian/ testing-updates main contrib non-free
>
> deb http://ftp.cn.debian.org/debian/ testing-proposed-updates main contrib non-free
> deb-src http://ftp.cn.debian.org/debian/ testing-proposed-updates main contrib non-free

源列表中，每一行是一个单位，每行中由多个字段组成，字段之间以**空白符**分割，使用井号（#）作为注释符。

- **第一字段** -- 包类型
该字段的取值有两个，deb 和 deb-src，分别对应二进制包和源码包。通常只有二进制包有用。

- **第二字段** -- 源,即镜像站点
该字段的 URL 可以定位到某个目录，在该目录下必须有 dists 和 pool 两个子目录。如 http://ftp.cn.debian.org/debian/.

- **第三字段** -- 指定包的版本类型
打开一个源，进入 dists 目录，里面的每一个子目录都是一个仓库，我们清楚地看到该源中有哪些仓库。子目录的命名方式为 系统发行版名-仓库名，比如 Debian 的 jessie-backport，其中没有仓库名的是版本仓库.
除了版本仓库之外还有以下几个仓库名:
	+ **updates**：指的是那些非安全性更新，即不影响到系统安全的 bug 修补.
	+ **proposed-updates**：提议(建议)更新，即小 beta 版。之后会进入 updates.
	+ **backports**：backport的含义是”向后移植”，就是将软件新版本的某些功能移植到旧版本上来,这种行为就称为backport.Backports是从testing版本 （大部分）和 unstable版本 (可能性极小,例如：安全更新等)重新编译的软件包,因此他们在稳定的debian发行版中不需要新的库就可以运行,当然,较新的软件包或许带来新的bugs.
- **第四字段** -- 软件的类型
它主要包括”自由软件（main）“、”半自由软件(contrib)“、”非自由软件（non-free）“三种类型。

了解了sources.list的书写规则,我们就可以自由的修改软件源了,执行下面的命令可以修改:
桌面环境下打开终端执行下面命令:
> $ gedit /etc/apt/sources.list

字符界面:
> $ nano /etc/apt/sources.list
> 更改完成后ctrl+o保存 ctrl+x退出

然后复制上方示例到这个文件中,**注意**此操作需要root权限.**注意**一定根据自己的Debian版本修改对应的第三字段,此外某些镜像中第三字段包的版本类型名称可能也需要修改.

## 示例
（**注**：不要**同时启用**多个源，同一仓库的源只启用一个即可，否则容易引起依赖地狱）
> deb http://ftp.cn.debian.org/debian/ testing main contrib non-free
>deb-src http://ftp.cn.debian.org/debian/ testing main contrib non-free
>
> deb http://ftp.cn.debian.org/debian/ testing-updates main contrib non-free
> deb-src http://ftp.cn.debian.org/debian/ testing-updates main contrib non-free
>
> deb http://ftp.cn.debian.org/debian/ testing-proposed-updates main contrib non-free
> deb-src http://ftp.cn.debian.org/debian/ testing-proposed-updates main contrib non-free

实际上，当你明白换源这件事情到底是在做什么的时候，你不再需要装完系统打开浏览器搜索源，复制。。。这种事情了你只需要记住本站点，然后打开Terminal（终端）敲一句命令。
> wget https://ilovesusu.github.io/debian -qO /tmp/debian && sudo sh -c 'cat /tmp/debian > /etc/apt/sources.list'