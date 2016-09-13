计算机基础知识
==============
gaikuo


###Hareware
----------------
1. 硬盘类型
```
 硬盘类型           信息传输速度
 IDE(已经淘汰)      MB/S 
 SATA1 2 3          200MB/S
 SCSI               200MB/S
 SSD                300MB/S
 DCIE               300MB/S
```
 
2. 电脑厂商
```
国内:神舟 紫光 方正(后两者已死) 
台湾:宏基 华硕
日本:富士通 sony 东芝  松下
欧美:惠普 IBM DELL APPLE
跨国:LENOVO
```

3. 商务笔记本介绍
```
主要特性:续航 稳定 安全,无显卡,中级配置
主要生产厂家:富士通 HP DELL THINKPAD
```

4. 军用笔记本介绍
```

```
###查询系统硬件设备信息
---------------------
1.查询cpu信息
```
cat /proc/cpuinfo
```
2.查询信息
```
free -m
```
3.查询信息
```
du -sh
```

4.查询信息
```
fdisk -l
```

###查询系统软件设备信息
---------------------
1.查询挂载的USB设备信息
```
lsusb
```
2.查询PCI的信息 (包括声卡 显卡 网卡 无线网卡 USB设备等)
```
lspci
```
3.查询linux系统内核信息
```
uname -a
uname -r
```
4.查询linux发行版信息
```
cat /etc/redhat-release
```

