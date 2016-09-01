lanmp编译安装
==============
-------------------
```
编译三部曲
1.配置编译环境 ./configure 
2.make
3.make install

```
install mysql 编译安装mysql
===========================
----------------------------
1.创建一个文件夹,用于存放mysql源码压缩包:
```
  命令mkdir /tmp/src/build -p
  #在根目录下递归创建tmp src build 三个文件夹
```

2.配置mysql编译环境
```
  2.1 groupadd mysql 创建一个mysql的用户组
  2.2 useradd -c "Mysql Server" -d /var/lib/mysql -r -g mysql -s /sbin/nologin mysql
  #创建用户Mysql Server,-c 用于用户全名 -d 创建存放Mysql Server库的目录; -r 创建一个系统账户; -g创建用户初始登录组的组名或者号码,组名必须已经存在,且组号码必须指代已经存在的组; -s 用户登录的shell名,笔记中代表表示不允许以shell名登录
  2.3 https://dev.mysql.com/downloads/mysql/5.5.html->select source code->about 20M size
  #找到mysql安装文件地址,并选择源码
  2.4 wget https://dev.mysql.com/get/Downloads/MySQL-5.5/mysql-5.5.51.tar.gz
  #利用wget下载mysql源码压缩包
  2.5 tar -zxvf mysql-5.5.51.tar.gz -C /tmp/src/build
  #解压mysql源码压缩包到 /tmp/src/build
  2.6 cd /tmp/src/build/mysql-5.5.51/
  #打开已经解压的mysql的源码文件夹
  2.7 yum install sudo libssh2-devel zip unzip crontabs GeoIP-devel gcc gcc-c++ cmake make automake autoconf libjpeg libjpeg-devel libpng libpng-devel freetype freetype-devel zlib zlib-devel glibc glibc-devel bzip2 bzip2-devel ncurses ncurses-devel curl curl-devel e2fsprogs e2fsprogs-devel krb5-devel libidn libidn-devel openssl openssl-devel openldap openldap-devel openldap-clients openldap-servers libtool cmake bison flex libmcrypt-devel ncurses ncurses-devel ncurses-libs pcre-devel libmcrypt libmcrypt-devel libxml2-devel curl-devel gd-devel t1lib-devel libc-client-devel pam-devel libxslt-devel libtool-ltdl-devel ImageMagick-devel tree screen dos2unix lrzsz wget vim sudo git htop iftop MySQL-python lsof
  #利用yum命令配置环境
  2.8 CFLAGS="-O3" CXX=gcc
  #给CFLAGS CXX定义值
  2.9 CXXFLAGS="-O3 -felide-constructors -fno-exceptions -fno-rtti"
  #
  2.10 准备cmake数据
  cmake -MYSQL_USER=mysql \  设置mysql的用户
-DCMAKE_INSTALL_PREFIX=/opt/mysql-5.5.51 \  设置mysql的预安装地址
  -MYSQL_UNIX_ADDR=/tmp/mysql.sock \  设置XX地址
  -MYSQL_DATADIR=/opt/mysql-5.5.51/data \ 设置存放mysql data的地址
  -DSYSCONFDIR=/opt/mysql-5.5.51/etc \  设置存放mysql etc的地址
  -DDEFAULT_CHARSET=utf8 \   设置mysql 字符编码集为UTF-8
  -DWITH_EXTRA_CHARSETS=all \  设置mysql为多字符集
  -DDEFAULT_COLLATION=utf8_general_ci \ 设置mysql默认XXX的字符编码为utf8_general_ci 
  -DWITH_INNOBASE_STORAGE_ENGINE=1 \  设置
  -DWITH_FEDERATED_STORAGE_ENGINE=1 \
  -DWITH_BLACKHOLE_STORAGE_ENGINE=1 \
  -DWITHOUT_EXAMPLE_STORAGE_ENGINE=1 \
  -DWITHOUT_PARTITION_STORAGE_ENGINE=1 \
  -DWITH_EMBEDDED_SERVER=1 \
  -DWITH_READLINE=1 \
  -DENABLED_LOCAL_INFILE=1 \
  -DWITH_SSL=system \
  -DENABLED_PROFILING=ON \
  -MYSQL_TCP_PORT=3306 \
  -DWITH_DEBUG=OFF \
  -DCURSES_LIBRARY=/usr/lib64/libncurses.so \
  -DCURSES_INCLUDE_PATH=/usr/include \
  -DENABLE_DTRACE=OFF
  2.11 make && make install 编译安装
```


3.mysql config   配置mysql的配置文件 
```
  3.1 mkdir /opt/mysql-5.5.51/tmp /opt/mysql-5.5.51/binlog /opt/logs/mysql -p 
  #在根目录下创建opt文件,并在opt下再次创建文件夹mysql-5.5.51与logs,最后在mysql-5.5.51下创建tmp 和 binlog 文件夹;在logs文件夹下创建文件夹mysql; -p表示递归创建
  3.2 chown mysql:mysql -R /opt/logs/mysql /opt/mysql-5.5.51/tmp /opt/mysql-5.5.51/binlog /opt/logs/mysql
  #给用户组,mysql创建写入的权限
  3.3 chmod 777 -R /opt/logs/mysql /opt/mysql-5.5.51/tmp /opt/mysql-5.5.51/binlog /opt/logs/mysql
  #给新创建的文件夹所有权限
  3.4 ln -s /opt/mysql-5.5.51 /opt/mysql
  #在文件夹mysql-5.5.51和文件夹mysql之间创建一个软连接,并指向mysql文件夹
  3.5 cp ./do_conf/mysql/my.cnf /etc/my.config
  #复制my.config文件
```

4.启用mysql 
```
4.1 cd /opt/mysql-5.5.51/scripts
#打开scripts文件夹
4.2 ./mysql_install_db --basedir=/opt/mysql-5.5.51/ --datadir=/opt/mysql-5.5.51/data/ --user=mysql
#./开头是执行shell脚本的标志.在执行前需要确认文件是否为shell脚本
4.3 cp ./do_conf/mysql/mysqld /etc/init.d/mysqld
#复制mysqld文件
4.4 chmod 0755 /etc/init.d/mysqld
#修改mysqld的权限为0755
4.5 cp ./do_conf/mysql/mysql.sh /etc/profile.d/mysql.sh
#复制mysql.sh到etc中的profile.d文件夹下,并重新命令为mysql.sh
4.6 chmod 0755 /etc/profile.d/mysql.sh
#修改mysql.sh的权限为0755
4.7 sh /etc/profile.d/mysql.sh
4.8 chkconfig --add mysqld
4.9 chkconfig --level 345 mysqld on
4.10 /etc/init.d/mysqld start 启用mysql
4.11 ln -s /opt/mysql-5.5.51/bin/mysqld_safe /usr/local/bin/
4.12 ln -s /opt/mysql-5.5.51/bin/mysqladoin /usr/local/bin/
4.13 ln -s /opt/mysql-5.5.51/bin/mysql /usr/local/bin/
4.14 mysqld_safe --user=mysql &
```

5.创建mysql的使用用户
```
5.1 mysqladoin -u root password 'password1'
5.2 mysql -u root -p
>use mysql;
>grant all privileges on *.* to root@'%' identified by 'password1' with grant option;
>grant all privileges on *.* to root@'127.0.0.1' identified by 'password1' with grant option;
>grant all privileges on *.* to root@'localhost' identified by 'password1' with grant option;
>flush privileges;

5.3 cp ./do_conf/mysql/mysqld /etc/init.d/mysqld #复制mysqld文件
5.4 chmod 0755 /etc/init.d/mysqld #修改mysqld的权限为0755
5.5 cp ./do_conf/mysql/mysql.sh /etc/profile.d/mysql.sh #复制mysql.sh到etc中的profile.d文件夹下,并重新命令为mysql.sh
5.6 chmod 0755 /etc/profile.d/mysql.sh #修改mysql.sh的权限为0755
5.7 sh /etc/profile.d/mysql.sh
5.8 chkconfig --add mysqld
5.9 chkconfig --level 345 mysqld on
5.10 /etc/init.d/mysqld start 启用mysql
5.11 ln -s /opt/mysql-5.5.51/bin/mysqld_safe /usr/local/bin/
5.12 ln -s /opt/mysql-5.5.51/bin/mysqladoin /usr/local/bin/
5.13 ln -s /opt/mysql-5.5.51/bin/mysql /usr/local/bin/
5.14 mysqld_safe --user=mysql &
```

