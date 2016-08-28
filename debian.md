debian
============

###安装
-------------
1.准备工作
‵‵‵
知晓电脑环境:64位/32位,好下载对应对数的debian版本软件
‵‵‵

2.选择安装方式
‵‵‵
一般有网络下载安装\U盘安装\虚拟机安装三种形式, 本文将详细说下U盘安装的过程.在开始安装以前你还需要下载版本一致的debian\vmlinuz\initrd.gr文件,并放入U盘中待用(放文件前U盘前要格式化)
‵‵‵

3.开始安装
```
a.文件放入U盘以后重启按F12进入安装界面
b.install
c.选择语言
d.选地域
e.选键盘
f.设置主机名,无需域名
g.设置root密码
h.设置帐号与帐号密码
j.设置disk分区,新手可选自动*1

注意*1 关于disk补充一些概念:disk包含sda物理硬盘 和sdb U盘两种形式,在分区的时候一般是将sda物理硬盘分为主分区与逻辑分区.主分区相当于windows中的C盘,逻辑分区则相当于win中的其他盘.而sdb U盘只要插上就自动挂载了. 
``` 

###系统配置
-------------
1.首要保证电脑连上网,设置电缆网络配置
```
手动配置ethernet
地址:IP地址 192.168.x.x
子网掩码:255.255.255.0
网关:
DNS servers:解释域名变成可识别IP地址
search domiains:判断跳转中转至某个站点
```

2.挂载软件
```
a.配置source.list文件,关闭2个cdrom命令和2个socuriety命令.
b.上网寻找无限网*1\声卡\显卡驱动,下载安装
c.到网页版仓库中下载自己需要的软件,这里推荐网易的一个仓库,地址为:mirrors.163.com/.help/debian.html
到这里,安装就算告一段落了.

3.安装字体 /usr/share/fonts -r
4.配置语言环境dpkg-reconfiger [space] locales

注意:*1装无限驱动的流程
1.lspci | grep Wireless  ls所有的pci设备并搜索无线设备,以获取硬件驱动型号(本机:BCM4313)
2.搜索网络关键字为"BCM4313 系统名称debian 驱动"
```

###debian命令
---------------
```
前言:命令都是小写,你首先要学会使用man 和 info命令查询帮助手册:man ls / info ls
,info比man更详细.--help是命令的帮助文件.~histroy 查看历史输入命令

1.PWd显示当前路径
2.ls 输出当前路径下的所有文件(不包含隐藏文件);la同左且包含隐藏文件
	ls -la | more  /  ls -la | less 分批显示查询内容
3.切换目录 cd
	cd – 回到最近一次使用目录
	cd ~ 回到用户家目录
	cd .. 回到父级目录
	cd ../..  回到父级的级目录
	cd 后跟一个绝对地址,直接进入文件夹

4.touch命令 创建文件 : touch filename
5.mkdir命令 创建文件夹: mkdir tmp/clare/js -p 递归创建不存在的中间目录
6.cat 输出文本内容 :   cat filename.txt / cat filename.txt -n 行号
	cat >  完全覆盖文本内容
      cat >> 追加文本的末尾,格式为另起一行
      cat /etc/debian-version 显示版本号
7.cp命令 复制文件及文件夹 :cp 被cp文件地址 复制目标地址
	cp -r 递归复制目录
	cp 文件夹1 文件夹2 将文件夹1的内容复制进文件夹2中,并变成文件夹2的下级
	cp 文件夹1/*/文件夹2 pg 将文件1的内容复制到文件夹中,并指定pg(后缀)
8.rm命令 删除文件以及文件夹: rm 文件名 删除文件
	rm -f 强制删除文件
	rm -rf 强制删除文件内所有内容 并不提示
9.apt命令  下载
	apt-get install package 安装包
	apt-get install package -rainstall 重新安装并修复
	apt-get remove 安装包
	apt-get remove -purge 删除包同时删配置文件
	apt-get install -f 补充缺失包
	apt-get clean 快速清除
	apt-get remove 清除旧包
	apt-get autoclean 自行清除
	有关下载更新的三个命令: 在安装时apt换成 aptitude更安全
		a.apt-get update 从网络库中将资源的地址找到
		b.apt-get upgrade 安装/升级找到的资源,并安装
		c. apt-get disk-upgrade -y更新debian系统
		d. apt-get update and apt-get upgrade -y 找到并下载安装/下载更新
        apt-cache search 搜索一个带关键词的包
	apt-get instopensssh -server  安装ssh服务 
		ssh clare@ipad 允许clare 远程登录 ipad (可执行下载/上传/安装等一切任务)

	 
10.date查询时间	
11.ifconfig 查询网络情况和网卡信息
12.管理系统应用服务: systemctl  stop/ start/ restart/ reload +对象(php)
13.界面控制快捷命令(一般为全局变量)
        A.设置位置: 狗图标 -> setting -> windows manager 

        B.界面缩放快捷键
        a.alt + F2 窗口横向放大,不增加竖向的大小
        b.alt + F3 窗口竖向放大,不增加横向的大小
        c.alt + F4 退出窗口
        d.alt + F7 移动窗口
        e.alt + F8 改变窗口大小
        f.alt + F10 全屏但保留最上菜单面板
        g.alt + F11 全屏不保留最上菜单面板
 
14.切换工作区快捷键命令
        a.win键+上下左右 窗口在工作区中移动
        b.control + alt + 上下左右 切换工作区
 
15.启动应用程序快捷键:添加 -> 输入linux命令 -> 输入快捷键; 例: win键+c 启动google-chorme
16.配置HDMI双屏幕:
        a.xrandr命令查看笔记本电脑屏幕(本机LVDS-0)与HDMI连接屏幕(如:HDMI-0)名称
        b.输入 xrandr --output HDMI-0 --right/left-of LVDS-0

```

###终端快捷命令
---------------
```
1. 开启终端:2way → ctrl+shift+t / ctrl+alt+t
2.终端全屏: alt+F10
3. 终端光标移动:
	ctrl+A移动到这一行的行首
	ctrl+E移动到这一行的行末
4.取消指令: ctrl+c
5.退出指令: ctrl+D
6.删除光标左边一个单词: ctrl+w


```



