有许多安装Node.Js的不同的方法。通过本篇文章我们将手把手带着你在Debian上安装Node.Js，在此之前请卸载旧版本的包以免发生包冲突。

这里介绍两种方式安装Node.js
* 用包管理器安装Node.Js
* 用NVM安装Node.Js

首先我介绍一些两种方式都是什么用途。
**假如你是一个Node.js的轻度使用者，比如你只是简单的使用一些Node.js的开发对的应用，例如使用Hexo，gitbook等应用，那么通过包管理器安装Node.Js是您的最佳选择。**
**假如你是一个Node.js的开发人员，需要测试代码在不同版本的Node.js中的表现，或者您要学习使用Node.js，那么通过用NVM安装Node.Js是您的最佳选择。**

## 用包管理器安装Node.Js
首先介绍一下Debian提供的两个包
nodejs：是由Debian相关人员将官方Node.Js打包的debian package
nodejs-legacy：以前有个叫node的包也提供了node这个命令导致冲突了，所以Debian官方暂时提供了nodejs-legacy这个软件包来提供nodejs到node的软链接，可以选择手动安装这个包，这样系统就有node这个命令了

介绍了这两个软件包，通过包管理安装Node.js就很简单了。
> sudo apt install nodejs nodejs-legacy

然后测试一下,看看nodejs的版本。
> nodejs -v
npm-v

## 用NVM安装Node.Js
这里也介绍一下NVM。
nvm 的全称是 Node Version Manager，之所以需要这个工具，是因为 Node.js 的各种特性都没有稳定下来，所以我们经常由于老项目或尝新等原因，需要切换各种版本。
安装nvm很简单
> curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash

执行完脚本后重新打开一个terminal测试一下
> command -v nvm
安装成功以后会返回“nvm”

通过下述命令查看node.js官方的lts版本。
> nvm ls-remote --lts

通过下述命令安装node.js官方的lts版本。
> nvm install v4.8.2（书写本文时lts是v4.8.2）

当您安装多个node.js版本需要切换是执行下述命令
> nvm use v6.10.2



