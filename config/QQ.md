## Debian QQ食用指南
其实网上很多人提供了好多方案，比如别人打包的 wine qq 8.5，或者使用的是 deepin 的 qq 。再者就是 vbox 里 xp 专门使用 QQ 。但是上述的方式在使用中都有或多或少的问题，真是不得不感叹”还是 Native 好啊！“。

## crossover
使用 CrossOver 可以在 Mac 和 Linux 运行您的 Windows 软件，从此摆脱双启动的繁琐和虚拟机的卡顿。让 Windows 办公软件、实用工具还有游戏都原生地运行在您的 Mac 和 Linux 上。因为 CrossOver 不像虚拟机一样需要安装一个完整的 Windows 系统，所以 Windows 程序得以高效运行、游戏得以获得更高的帧数，并且您也无需再购买 Windows。

CodeWeavers 所做的一切都是围绕开源的 Wine 项目展开的。他们将有关 Wine 的所有代码反馈给 Wine 项目。事实上，来自 CodeWeavers 的开发者为 Wine 贡献了 2/3 的代码。他们针对 Wine 的大部分改进，在集成进 CrossOver 之前，都是首先提交到 Wine 上游的。

#### 安装crossover
1. 通过[链接](https://www.codeweavers.com/products/crossover-linux)下载crossover（需要提供邮箱）
2. 如果你使用64位 Debian 操作系统开启 Debian 32位架构支持
> $sudo dpkg –add-architecture i386

3. 安装crossover.deb
> $dpkg -i crossover.deb

#### 通过crossover安装QQ

1. 打开crossover点击安装windows软件，然后搜索QQ，选择QQ8.9
2. 根据提示操作，很容易成功安装QQ


## wineqq
Wine （“Wine Is Not an Emulator” 的首字母缩写）是一个能够在多种 POSIX-compliant 操作系统（诸如 Linux，macOS 及 BSD 等）上运行 Windows 应用的兼容层。 Wine 不是像虚拟机或者模拟器一样模仿内部的 Windows 逻辑，而是將 Windows API 调用翻译成为动态的 POSIX 调用，免除了性能和其他一些行为的内存占用，让你能够干净地集合 Windows 应用到你的桌面。

#### 安装wine
1. 如果你使用64位 Debian 操作系统开启 Debian 32位架构支持
> $sudo dpkg –add-architecture i386

2. 安装wine非常简单，执行下面的命令
> $sudo apt-get install wine

#### 通过wine安装QQ
1. 首先通过链接下载[安装包](http://pan.baidu.com/s/1kVgxs3t)
2. 安装下载的 QQ *** .deb包(***表示软件包名称)
> $dpkg -i ***.deb

## virtualbox
VirtualBox是用于企业和家庭使用的强大的x86和AMD64 / Intel64 虚拟化产品。VirtualBox不仅是企业客户极富功能的高性能产品，同时也是根据GNU通用公共许可证（GPL）版本2，免费提供的开源软件专有解决方案。

目前，VirtualBox在Windows，Linux，Macintosh和Solaris主机上运行，​​并支持大量的客户机操作系统，包括但不限于Windows（NT 4.0,2000，XP，Server 2003，Vista，Windows 7，Windows 8，Windows 10 ），DOS / Windows 3.x，Linux（2.4,2.6,3.x和4.x），Solaris和OpenSolaris，OS / 2和OpenBSD。

#### 安装virtualbox
Debian 下安装virtualbox很简单,详细请看常用软件推荐。
> sudo apt install virtualbox

#### 通过virtualbox安装windows
> 请移步[virtualbox篇]()

安装好windows系统以后安装QQ就不用多说了吧！



