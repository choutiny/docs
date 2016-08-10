github
============

###安装
-------------
```
1.打开终端
2.切入root模式
3.输入apt-get update and apt-get upgrade git y
4.等它自己下载安装
```

###配置
-------------
```
1.用户名设置 

git config --system user.name "choutiny" 
git config --global user.name "choutiny" git config user.name "choutiny" 
2.电子邮件设置 
git config --global user.email "choutiny@gmail.com" 
3.设置文本编辑器，默认为vi,看你用什么编辑器 
git config --global core.editor vim 
4.查看配置信息 
git config --list 
	如果要查看某个特定的环境变量，只要把它的名字放到最后即可 
	git config user.name 

```

###建立裸仓库  get init
-------------
```
clare@debian:~$ cd ../www/test
clare@debian:/home/www/test$ 
clare@debian:/home/www/test$ git init
Initialized empty Git repository in /home/www/test/.git/
clare@debian:/home/www/test$ cd .git
clare@debian:/home/www/test/.git$ ls -la
clare@debian:/home/www/test/.git$ vim config 
clare@debian:/home/www/test$ git rev-parse --git-dir.git




```



###命令
-------------
```
git add  添加所有的文件到索引
git commit 向本地源码库提交，会打开默认vi编辑器写 “注释”
git push  把本地源码库push到Github上
git pull  从Github上pull到本地源码库
git rm
git mv
```


  
