## 安装Debian

这时候你肯定在Debian官网上下载好了网络安装CD或者完整DVD镜像，DVD镜像只需DVD-1即可。  
下载好镜像后做成U盘启动盘，从U盘启动开机。

在引导界面选择Install（字符界面安装）或Graphical install（图形化安装），进入安装过程。

![](/img/install1.png)

选择安装界面的语言，这里我选择中文或英语。

![](/img/install2.png)

这里提示您选择的语种翻译有可能不完整，让你重新选择一种安装时提示界面的语言，直接选是，下一步。

![](/img/install3.png)

区域选择，选择中国。

![](/img/install4.png)

主机名，随便写吧。

> 这里就是决定以后你的终端现实是：用户名@主机名:~$

![](/img/install5.png)

域名不用填以后可以设置，直接下一步。

![](/img/install6.png)

设置root密码，这里最好是设置一个强密码，比如sbEY.DF+GWEA。

![](/img/install7.png)

建立新用户，这个只是普通用户的用户名，可以根据自己喜好填。

![](/img/install8.png)

这里就是新用户的密码。

![](/img/install9.png)

接下来该磁盘分区了。

![](/img/install10.png)

关于怎么分区，[看这里](\)。

![](/img/install11.png)

![](/img/install12.png)

手动分区时，一定要记住挂载/根目录。

Swap分区（交换分区）推荐大小为物理内存的两倍，比如我的实际内存为2G，swap给上4G就行了。

完成调整后保存分区表即可。

需要注意的是需要记住挂载 根目录/ 的分区号，方便后面安装grub。

![](/img/install13.png)

选是则确定修改硬盘分区（这时考虑清楚，尤其是双系统的）。

![](/img/install14.png)

对于软件包流行度调查，随便你参加不参加都行。

![](/img/install15.png)

不用扫描其他DVD，不使用网络镜像。

如果网络环境不错的，选择Asia的China中选ftp.cn.debian.org。

![](/img/install16.png)

如上图，选择合适的软件包进行安装。

![](/img/install17.png)

安装完成后就是配置Grub了，如果你不想用Grub替换MBR，就选手动输入。

然后输入你前面配置的挂载根目录/的文件系统，像我前面用的是/sda1，这里就输入/dev/sda1。

![](/img/install18.png)

安装完成后，拔掉启动U盘，直接点继续。

