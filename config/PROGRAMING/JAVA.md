## 一. 安装jdk 

Debian6以后安装SunJdk不只是简单的使用apt-get install 了，因为一些原因，Debian不维护SunJdk的deb了 所以只能从jdk官方下载压缩包安装。
某次在Debian wiki上浏览的时候发现了一个包，是java-package，所以我去查了查。
大家可以看看下面的链接。
> [java-package](https://packages.debian.org/stretch/java-package)

1. Download java jdk from oracle [website](/http://www.oracle.com/technetwork/java/javase/downloads)
1. Install java-package from debian repos using command “apt-get install java-package”
1. Run this command to create .deb file “make-jpkg jdk-8u45-linux-x64.tar.gz”
1. Install .deb file using “dpkg -i oracle-java8-jdk_8u45_amd64.deb”
1. Run this command to check java version “java -version”

这样就能apt管理这个jdk了。

## 二. 需要配置的环境变量 

1. 修改.bash_profile文件 
> export JAVA_HOME=/usr/share/java
export PATH=$JAVA_HOME/bin:$PATH 
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar 

## 三. 测试jdk

1. 用文本编辑器新建一个Test.java文件，在其中输入以下代码并保存：

```
public class test {
public static void main(String args[]) {
System.out.println("A new jdk test !");
}
}
```

1. 编译：在shell终端执行命令 javac Test.java
1. 运行：在shell终端执行命令 java Test

当shell下出现“A new jdk test !”字样则jdk运行正常。

## 四. 卸载jdk 
可以直接通过apt卸载
