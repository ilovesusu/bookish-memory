由于网络封锁，YouTube、Facebook、Twitter、Blogger、WordPress、Google……全世界最好的网站和服务，一个个远离中国，它造就了我们这个时代中国人最大的悲哀。由于网络封锁，大陆网民最悲哀也是最唯一的选择，只能是通过一些手段 去获取信息。翻墙即就是翻越长城防火墙（GWF）。

翻墙教程很多，所采取的方法也很多，有免费的，也有收费的。我下面推荐几种方法大家可以一试。

1. xx-net
2. shadowsocks
3. Lantern
4. hosts

## xx-net
### 安装
[直接看xx-net wiki](/https://github.com/XX-net/XX-Net/wiki/%E4%B8%AD%E6%96%87%E6%96%87%E6%A1%A3)

## shadowsocks

**Shadowsocks**（中文名称：影梭）是使用Python等语言开发的、基于Apache许可证开源的代理软件。 Shadowsocks使用Socks5代理，用于保护网络流量。 在中国大陆被广泛用于突破防火长城（GFW），以浏览被封锁的内容。 Shadowsocks分为服务器端和客户端。
### 安装
Shadowsocks的安装是直接执行下述命令直接从debian源中安装。
> sudo apt update && sudo apt install shadowsocks

### 配置Shadowsocks server端
配置文件为：/etc/shadowsocks-libev/config.json，格式说明：
> ``` json
{
	"server":"example.com or X.X.X.X",
	"server_port":443,
	"password":"password",
	"method":"rc4-md5",
	"timeout":60
}
```
其中：
> server：主机IP
server_port：服务器监听端口
password：密码
method：加密方式 默认为table,其他有rc4,rc4-md5,aes-128-cfb, aes-192-cfb, aes-256-cfb,bf-cfb, camellia-128-cfb, camellia-192-cfb,camellia-256-cfb, cast5-cfb, des-cfb

## 配置Shadowsocks client端
将下面的脚本保存后执行，比如我保存到/home/susu/ss.sh
> $./ss.sh

然后执行脚本就可以。

> \#! /bin/bash
sslocal -s server_ip -p 8388  -l 1080 -k password -t 600 -m aes-256-cfb

### 配置浏览器
firefox配置很简单在设置--》网络  
在代理里面选择socks 然后填 127.0.0.1:1080
chrome配置需要安装SwitchySharp
首先 点击[这里下载 谷歌 SwitchySharp 浏览器插件](./142137644SwRsBaO.zip),下载后,解压zip 文件,可以看到文件 Proxy_SwitchySharp.crx .
1. 点击谷歌浏览器最右边的下拉图标， 选择“更多工具” - “扩展程序” ， 将文件 Proxy_SwitchySharp.crx  拖入到 谷歌浏览器 扩展程序的界面中， 点击“添加扩展程序” 按钮， 添加“谷歌 SwitchySharp”插件。
2. 在"SwitchSharp选项" 中选择 “手动配置”，  SOCKS代理 输入  localhost  端口号输入刚才在shadowsocks中配置的代理端口: 1080 ， 点击保存。
3.点击谷歌浏览器右边的SwitchySharp插件的图标,下拉菜单中,选择自己设定的名字，即可使用翻墙网络，打开网址：google.com，如果能使用google正常搜索，shadowsocks配置成功。


## Lantern

**Lantern**是一个免费的对等网络审查回避工具，用于随意的网络浏览。它提供了一种通过受信任用户网络绕过状态验证过滤的方法，它不是一个像Tor的匿名工具。使用Lantern，有免费互联网接入的用户可以在网络中与部分被阻塞的国家的用户共享带宽。网络连接将分散在运行Lantern的多台计算机之间，因此不会对单个连接或计算机施加过度的压力。

安装很简单就是打开下述网址，然后选择对应位数的deb软件包下载安装即可。
> [这里](https://github.com/getlantern/forum/issues/833)

## hosts

Hosts是一个/etc目录下的系统文件，其作用就是将一些常用的网址域名与其对应的IP地址建立一个关联“数据库”，当用户在浏览器中输入一个需要登录的网址时，系统会首先自动从Hosts文件中寻找对应的IP地址，一旦找到，系统会立即打开对应网页，如果没有找到，则系统会再将网址提交DNS域名解析服务器进行IP地址的解析。

在这里推荐使用这个[google hosts](https://github.com/racaljk/hosts
) 

这里提供一句命令快速修改hosts文件
> wget https://raw.githubusercontent.com/racaljk/hosts/master/hosts -qO /tmp/hosts && sudo sh -c 'cat /tmp/hosts > /etc/hosts'

然后输入密码即可修改hosts文件
