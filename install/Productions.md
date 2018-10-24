## 制作启动U盘

> 这篇文章分别介绍Debian以及windows下面几种制作u盘系统启动的方法，使用的iso系统文件为Debian -xxx.iso官方版本。

### 如果是windows，方法如图所示

#### UNetbootin
1. 首先去[这里](/https://unetbootin.github.io/)下载win版本的Netbootin
软件。
2. 运行下载好的Netbootin软件。![](/img/Netbootin.png)
3. 选择好发行版，点击上图的...按钮选择下载好的Debianxxx.iso文件。
4. 然后点击确定，开始刻录，等待一段时间后完成。

#### UltraISO
1. 百度找一个这个软件吧！毕竟收费的软件，我不怎么用。破解的地址我就不给了。
2. 首先我们先安装软碟通，完成安装后打开软碟通，文件->打开，打开我们的iso镜像。![](/img/UltraISO1.jpg)
3. 然后选择我们的U盘![](/img/UltraISO2.jpg)
4. 然后点击启动->写入硬盘映像![](/img/UltraISO3.jpg)
5. 写入方式有zip和hdd两种，一般我们选择hdd或hdd+，选择了写入方式之后要先格式化，格式化完毕之后点击写入等待写入完毕即可![](/img/UltraISO4.jpg)

### 如果是Linux，就用dd命令
 
dd 是 Linux/UNIX 下的一个非常有用的命令，作用是用指定大小的块拷贝一个文件，并在拷贝的同时进行指定的转换。

1. dd命令简单用法就是这样，可以用它烧写光盘和作其他系统的启动U盘。
> $ sudo dd bs=4M if=~/debian-wheezy.iso of=/dev/sdb && sync

2.使用dd命令备份整个硬盘。源硬盘的设备名为/ dev/ sda的，目标硬盘的设备名是/ dev/ sdb。执行dd命令，备份整个硬盘/dev/sha到同一系统的另一个硬盘/dev/sdb。"if"后跟输入文件，“of”后跟输出文件。如下所示：
> $ dd if=/dev/sda of=/dev/sdb

3.
