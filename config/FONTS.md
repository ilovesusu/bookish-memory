在安装debian系统的时候如果选择使用中文作为操作系统的字体，但在安装过程中并没有联网进行同步更新，那么很可能在debian系统安装成功以后出现所有中文文字都是小方块数字字母及黑块问号的情况（像麻将上放者四个小字）。出现这种情况的原因是因为系统的安装时候没有安装中文的字体库，罗列一些解决方法如下：

## 安装X Window字体包
使用apt-get install xfonts-intl-chinese命令来获取字体包并安装即可，这些字体可用于X Window系统。
## Debian中文设置
- 安装 Local
> aptitude install locales

- 然后执行下述命令，跳出一个文字选择界面（如果安装时选择中文，此时文字全是乱码）。
> dpkg-reconfigure locales

- page up/dn 翻页、空格键选择以下编码
> en_US.UTF-8 UTF-8
zh_CN.GBK GBK
zh_CN.GB2312
zh_CN.UTF-8 UTF-8

然后 Tab 键切换到 OK，最后默认语言选择 en_US.UTF-8

## 推荐几款字体
### 中文字体
（注：可以直接通过apt安装）
- xfonts-wqy （文泉驿）
- fonts-wqy-* （文泉驿）
- fonts-noto-cjk （思源）
### 编程字体
- fonts-hack-ttf 
- Source Code Pro（https://github.com/adobe-fonts/source-code-pro）
- Iosevka（https://github.com/be5invis/Iosevka）
- FiraCode （https://github.com/tonsky/FiraCode）