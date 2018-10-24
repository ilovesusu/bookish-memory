## LAMP 环境的搭建

LAMP是一组用于搭建网站的开源软件。LNMP代表Linux操作系统、Apache HTTP服务器、MySQL/MariaDB数据库和PHP。在这篇教程中，我将介绍如何在Debian 8 服务器上安装LAMP。数据库选择MariaDB, 并安装最新的PHP7. 以下命令在Debian服务器上执行.

### 安装Apache

Apache HTTP Server是Apache软体基金会的一个开放原始码的网页伺服器软体，可以在大多数电脑作业系统中运行，由于其跨平台和安全性。被广泛使用，是最流行的Web伺服器软体之一。它快速、可靠并且可通过简单的API扩充，将Perl／Python等直译器编译到伺服器中

> $sudo apt-get install apache2  -y

- 运行Apache状态
安装完成后，Apache会自动运行。查看运行状态执行下面的命令.

> $ systemctl status apache2.service
> ...\(部分内容忽略\)  
> Active: active \(running\)\(这就表示运行了apache2\)  
> ...

- 查看Apache版本

> $ apache2 -v  
> Server version: Apache/2.4.25 (Debian)
Server built:   2017-01-25T22:59:26

在浏览器地址栏中输入Debian服务器的IP或者本地浏览器查看127.0.0.1, 回车。如果你看到下面的页面，说明Apache安装好了.

![nginx-welcome](/service/img/apache-welcome.png)

### 安装MariaDB

MariaDB是MySQL的一个替代品。使用下面的命令安装：

> sudo apt-get install -y mariadb-server mariadb-client

在安装过程中会要求你为MariaDB root用户设置一个密码。输入密码后按回车。  
**注意:**MariaDB root是指数据库的管理员,并非Linux root用户.

- 查看MariaDB版本
> $ mysql --version
mysql  Ver 15.1 Distrib 10.1.23-MariaDB, for debian-linux-gnu (x86_64) using readline 5.2

- 执行安全脚本
安装完mysql-server 会提示可以运行mysql_secure_installation。运行mysql_secure_installation会执行几个设置：
    1. 为root用户设置密码
    2. 删除匿名账号
    3. 取消root用户远程登录
    4. 删除test库和对test库的访问权限
    5. 刷新授权表使修改生效
通过这几项的设置能够提高mysql库的安全。建议生产环境中mysql安装完成后**一定要运行一次**mysql_secure_installation，详细内容请参看下面的回显:
> $ mysql_secure_installation
NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MySQL
SERVERS IN PRODUCTION USE! PLEASE READ EACH STEP CAREFULLY!
In order to log into MySQL to secure it, we'll need the current
password for the root user. If you've just installed MySQL, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.
Enter current password for root (enter for none):<–初次运行直接回车
OK, successfully used password, moving on…
Setting the root password ensures that nobody can log into the MySQL
root user without the proper authorisation.
Set root password? [Y/n] <– 是否设置root用户密码，输入y并回车或直接回车
New password: <– 设置root用户的密码
Re-enter new password: <– 再输入一次你设置的密码
Password updated successfully!
Reloading privilege tables..
… Success!
By default, a MySQL installation has an anonymous user, allowing anyone
to log into MySQL without having to have a user account created for
them. This is intended only for testing, and to make the installation
go a bit smoother. You should remove them before moving into a
production environment.
Remove anonymous users? [Y/n] <– 是否删除匿名用户,生产环境建议删除，所以直接回车
… Success!
Normally, root should only be allowed to connect from 'localhost'. This
ensures that someone cannot guess at the root password from the network.
Disallow root login remotely? [Y/n] <–是否禁止root远程登录,根据自己的需求选择Y/n并回车,建议禁止
… Success!
By default, MySQL comes with a database named 'test' that anyone can
access. This is also intended only for testing, and should be removed
before moving into a production environment.
Remove test database and access to it? [Y/n] <– 是否删除test数据库,直接回车
\- Dropping test database…
… Success!
\- Removing privileges on test database…
… Success!
Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.
Reload privilege tables now? [Y/n] <– 是否重新加载权限表，直接回车
… Success!
Cleaning up…
All done! If you've completed all of the above steps, your MySQL
installation should now be secure.
Thanks for using MySQL!

MariaDB数据库安装完成。

### 安装PHP7

安装PHP很简单,使用下面的命令安装:

> apt-get install php php-mysql php-fpm 

### 设定 php.ini

安裝完了之後，我們接下來要去設定 php.ini 的一個小地方，以防止資安事件。
參考資料：[Nginx + PHP CGI的一个可能的安全漏洞](http://www.laruence.com/2010/05/20/1495.html)

> vi /etc/php5/fpm/php.ini
请取消 cgi.fix_pathinfo=1 的注解，并把默认值改为 0 （如下所示）

``` 
php.ini
; cgi.fix_pathinfo provides *real* PATH_INFO/PATH_TRANSLATED support for CGI.  PHP's
; previous behaviour was to set PATH_TRANSLATED to SCRIPT_FILENAME, and to not grok
; what PATH_INFO is.  For more information on PATH_INFO, see the cgi specs.  Setting
; this to 1 will cause PHP CGI to fix its paths to conform to the spec.  A setting
; of zero causes PHP to behave as before.  Default is 1.  You should fix your scripts
; to use SCRIPT_FILENAME rather than PATH_TRANSLATED.
; http://php.net/cgi.fix-pathinfo
cgi.fix_pathinfo=0
```
保存文件后重启php7.0-fpm
> systemctl restart php7.0-fpm.service

### 配置Apache Virtual Host

在/etc/apache2/sites-available目录下创建一个新的virtual host配置文件

> vi /etc/apache2/sites-available/your-domain.conf
将your-domain替换成你实际的域名。然后在文件中修改下面的配置。
```
aa
```
保存文件后，

> 

测试Apache配置
> apache2 -t

测试成功：

```
Syntax OK
```

重新加载apache2配置
> systemctl reload apache2.service

将/var/www/html目录的所有者更改为Apache用户www-data
> chown www-data:www-data /var/www/* -R

### 测试PHP

在/var/www/html/目录下新建一个文件info.php

vi /var/www/html/info.php
将下面的内容粘贴到info.php文件中。
<?php
   phpinfo();
?>
保存文件。然后在浏览器的地址栏输入下面的地址。
> your-domain.com/info.php

用你的实际域名替换your-domain.com. 如果你看见下面的文字，说明PHP运行正常。
![](/service/img/phpinfo.png)

