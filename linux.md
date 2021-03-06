##linux note
================

系统目录结构
--------------------
```
1. /bin:
bin是存放最经常使用的命令
2./boot:
存放启动linux时使用的一些核心文件,包括一些连接文件以及镜像文件。
3./dev:
dev是Device(设备)的缩写, 该目录下存放的是Linux的外部设备，在Linux中访问设备的方式和访问文件的方式是相同的
4./etc:
这个目录用来存放所有的系统管理所需要的配置文件和子目录
5./home:
用户的主目录，在Linux中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的
6./lib:
这个目录里存放着系统最基本的动态连接共享库，其作用类似于Windows里的DLL文件。几乎所有的应用程序都需要用到这些共享库
7./opt:
这是给主机额外安装软件所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下默认是空的
8.
/root：
该目录为系统管理员，也称作超级权限者的用户主目录
9./sbin：
s就是Super User的意思，这里存放的是系统管理员使用的系统管理程序
10./sys：
 这是linux2.6内核的一个很大的变化。该目录下安装了2.6内核中新出现的一个文件系统 sysfs,sysfs文件系统集成了下面3种文件系统的信息：针对进程信息的proc文件系统、针对设备的devfs文件系统以及针对伪终端的devpts文件系统
 11./tmp：
这个目录是用来存放一些临时文件的
12./usr：
 这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似与windows下的program files目录
13./usr/bin：
系统用户使用的应用程序
14./usr/sbin：
超级用户使用的比较高级的管理程序和系统守护程序
15./usr/src：内核源代码默认的放置目录
16./var：
这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件
17./selinux：
 这个目录是Redhat/CentOS所特有的目录，Selinux是一个安全机制，类似于windows的防火墙，但是这套机制比较复杂，这个目录就是存放selinux相关的文件的
18./srv：
 该目录存放一些服务启动之后需要提取的数据
19./media linux系统会自动识别一些设备，例如U盘、光驱等等，当识别后，linux会把识别的设备挂载到这个目录下
20./mnt：
系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在/mnt/上，然后进入该目录就可以查看光驱里的内容了
21./selinux：
 这个目录是Redhat/CentOS所特有的目录，Selinux是一个安全机制，类似于windows的防火墙，但是这套机制比较复杂，这个目录就是存放selinux相关的文件的
22./srv：
 该目录存放一些服务启动之后需要提取的数据
23./lost found:
这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件
```


用户和用户组管理
--------------------
```
概括:Linux系统是一个多用户多任务的分时操作系统，任何一个要使用系统资源的用户，都必须首先向系统管理员申请一个账号，然后以这个账号的身份进入系统。每个用户账号都拥有一个惟一的用户名和各自的口令。用户在登录时键入正确的用户名和口令后，就能够进入系统和自己的主目录。
1.添加新用户
        useradd 选项 用户名
        选项: -c comment 指定一段注释性的描述
             -d 指定用户主的目录,如果不存在,同时使用-m可以创建主目录
             -g 用户组 指定用户所属的用户组
             -G 用户组,用户组指定用户所属的附加组
             -s shell文件 指定用户登录的shell
             -u 用户号 指定用户的用户号,如果同时有-0选项,则可以重复使用其他用户的标示号

```

快捷键
--------------------
```
1.找到笔记文件目录
a. cd www
b. ls
c. cd git
d. ls
e. cd docs
f. ls
g.gvim 文件名打开文件

2.界面控制快捷命令(一般为全局变量)
A.设置位置: 狗图标 -> setting -> windows manager 

B.界面缩放快捷键
 a.alt + F2 窗口横向放大,不增加竖向的大小
 b.alt + F3 窗口竖向放大,不增加横向的大小
 c.alt + F4 退出窗口
 d.alt + F7 移动窗口
 e.alt + F8 改变窗口大小
 f.alt + F10 全屏但保留最上菜单面板
 g.alt + F11 全屏不保留最上菜单面板
 
3.切换工作区快捷键命令
 a.win键+上下左右 窗口在工作区中移动
 b.control + alt + 上下左右 切换工作区
 
4.启动应用程序快捷键:添加 -> 输入linux命令 -> 输入快捷键; 例: win键+c 启动google-chorme

5.pwd  查看当前目录
6.root的家目录是 /root ,其他用户的家目录为home+用户名: /home/clare  |  /home/tommy
7.ps aux | grep 关键词 查询XXX的进程    ps aux | grep mysql 查询mysql的进程(检查是否启动)
8.scp 准备传送文件的绝对路径+文件名 root@192.168.0.1:传过去的绝对地址+新的名字
  scp -r 准备传送文件夹的绝对路径+文件夹名 root@192.168.0.1:传过去的绝对地址
  在本地, 把文件[夹]传送到远程服务器
        scp [-P port_num] [-r] ./relative_path/ remote_account@remote_ip:remote_path
        e.g:
           scp ./1.txt root@192.168.100.200:/tmp 
           scp -r /etc/php/ root@192.168.100.200:/tmp
           scp -P27329 ./1.txt root@192.168.100.200:/tmp  
  在本地, 把远程服务器的文件[夹]传送到本地
        scp  [-P port_num] [-r] remote_account@remote_ip:remote_path locate_path[file]
        e.g:
           scp root@192.168.100.200:/home/www/index.php /var/www 
           scp -r root@192.168.100.200:/home/www/ /var/www 
           scp -P22 -r root@192.168.100.200:/home/www/ /var/www

9. 家中服务器地址:xxx.187.52.223 
10.自动校对时间:  ntpdate
        
         安装:apt-get install ntp ntpdate
        
11.watch 的使用方式:
        watch -d -n3 'date +%F\ %H:%M:%S'
        延伸用法: 每隔数秒检查一次进程 ->   watch -d -n3 'ps aux | grep php'

```

