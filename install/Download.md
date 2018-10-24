## 学会用Jigdo下载 {#h2_0}

获取Debian ISO映象文件通常是一个痛苦、缓慢而且低效的过程。Jigdo是一种以容易、快速且非常有效的方式获取Debian ISO文件的新工具。Jigdo是一个非常通用的工具，并没有特别地与Debian ISO结合在一起。Jigdo可以用于制作任何提供类似Debian ISO文件那样容易、快速和有效的下载方式的ISO文件。

Jigdo（代表着“Jigsaw Download”），为Richard Atterer所写并且发布于GNU GPL条款之下。它是一个进行有效下载和更新ISO映像的工具。任何ISO映像。Jigdo不是Debian所特有的，然而Debian选择它作为下载 ISO映像的指定方法。Jigdo工具包含两个工具：jigdo-file为下载准备一个ISO映像，而jigdo-lite用于下载jigdo- file所准备的ISO映像。

### Jigdo是什么

Jigdo不生成ISO映像。它只是简单地准备它们并下载它们。ISO映像需要预先制作，这通常由mkisofs或debian-cd完成。

Jigdo通过两种获取Debian ISO映像的方法来解决所有的问题：

* 更快地下载整个ISO映像。

* 不象下载整个ISO映像，它可以使一个过时的CD映像（或者一个loop安装的过时的ISO映像）只下载那些自从创建这个CD（或ISO映像）改动过的文件并创建一个更新过的ISO映像。与你使用cvs更新源代码非常相似。

* jigdo-lite比PIK更容易使用。

显然，jigdo是获取Debian ISO映像的最佳方法。

### Jigdo如何工作

jigdo拥有两个组成部分：

jigdo-file：为下载准备ISO文件（由提供ISO文件的人使用）

jigdo-lite：下载ISO文件（由下载ISO文件的人使用）

### 安装Jigdo

Debian系都可以打开终端执行这个命令

> $ sudo apt-get install jigdo-file

### 使用jigdo下载镜像文件



### 使用jigdo更新镜像文件



