# 1.基础篇

## 1.1 linux文件系统

```
首先搞清楚linux的文件系统，理解一切皆文件，熟悉每一个文件夹是什么
```

* /bin
  * 存放最基础的命令：ls、cp、mv等
  * 系统启动就必须用到
* /sbin
  * s,system，存放管理员才能用的命令
  * 普通用户一般不能直接执行
* /boot
  * 系统启动文件：内核，grub引导程序
  * 别动这里，容易开不了机
* /dev
  * 设备文件:硬盘、鼠标等都在这里
  * 例如/dev/sda是第一块硬盘
* /etc
  * 所有配置文件都在这
  * 网络、用户、服务、开机启动脚本
* /home
  * 普通用户的家目录
  * 你登录后默认就在这里，如/home/zhangsan
* /root
  * root管理员的家目录
  * 和普通用户分开，更安全
* /lib
  * 系统运行需要的库文件
  * 类似Windows的DLL
* /usr
  * Unix Software Resource
  * 安装的软件、工具、文档大多在这里，/usr/bin、/usr/local，自己装软件常用
* /opt
  * 可选安装目录
  * 一般放大型软件:idea、docker、第三方大程序
* /tmp
  * 临时文件
  * 重启会清空，别存重要东西
* /var
  * 经常变化的文件
  * 日志/var/log，邮件、缓存、数据库文件
* /media/mnt
  * 挂载U盘、移动硬盘、光盘的地方
  * /mnt常用作手动挂载
* /proc
  * 虚拟文件系统，显示系统状态
  * 进程、CPU、内存信息都在这里
  * 不是真实文件，是内核实时数据
* /sys
  * 硬件相关的虚拟文件系统
  * 比/proc更偏硬件



## 1.2 vim编辑器

整体介绍

```
三种模式：普通模式、插入模式和命令行模式
```

* 普通模式

```
vim的默认模式、控制模式
用来移动光标、文本的复制、删除，核心是不直接编辑内容，而是操作文本

移动光标
复制：yy（复制当前行），3yy（复制3行）
粘贴：p（光标后粘贴）、p（光标前粘贴）
删除/剪切：dd（删除当前行）、x（删除光标所在字符）
撤销：u
重做：Ctrl+r

移动光标
指定行：4G
下一个单词：w
删除当前词：dw
跳到第一行：G
末尾行：gg
```

* 插入模式

```
直接编辑输入修改文本内容

进入方式:
i（insert）：在光标当前位置插入
a（add）:在光标下一个位置插入
o（one line）：在光标下一行新建一行并插入
I：跳到行首插入
A：跳到行尾插入
O：跳到上一行插入
```

* 命令行模式

```
vim的功能模式，用来执行高级指令（保存、退出、查找替换、设置vim参数等，所有指令以：开头）

进入方式：按：(冒号)、/（查找）、?(反向查找)等符号触发

查找:/关键词（向下找）、？关键词（向上找），按n下一个，N上一个
替换：:%s/旧内容/新内容/g(全文替换，%全文，g每行所有匹配)
显示行号：:set nu
隐藏行号：:set nonu
```

## 1.3 网络配置

VMware提供了三种网络连接模式：

* 桥接模式

```
虚拟机直接连接外部物理网络的模式，主机起到了网桥的作用。在这种模式下，虚拟机可以直接访问外部网络，并对外部网络是可见的


用自己的话来说：
桥接模式相当于，你有一个路由器连接外网(Internet),你自己用的电脑上面安装了一个虚拟机，这个时候你自己的主机充当了一个网桥的角色，看起来这个虚拟机像是一台真正的主机，与你的主机同等地位，是平行的。这个虚拟机拥有路由器动态分配的ip地址(消耗一个路由器的ip地址)，所以它可以通过路由器直接访问外网(Internet)，也可以被外网(Internet)或者局域网内的其他设备访问，这样就不够私密了
```

* NAT（网络地址转换）模式

```
虚拟机和主机构建的一个专用网络，并通过虚拟网络地址转换（NAT）设备对IP进行转换，虚拟机通过共享主机IP可以访问外部网络，但外部网络无法访问虚拟机

用自己的话来讲：
自己的主机有一张真实的网卡，在此基础上又虚拟了一张网卡，也虚拟了一个NAT服务器和DHCP服务器（虚拟路由器），你的虚拟机就与这个虚拟的路由器连接，虚拟机的ip就是由这个虚拟的路由器分配的。就像是局域网里面的局域网
```

* 仅主机模式

```
虚拟机只与主机共享一个专用网络，与外部网络无法通信

用自己的话来讲：
原先由虚拟路由器连接，现在变成是一个虚拟的交换机，相当于主机和虚拟机构成了一个内网，这个虚拟机只能和本主机通信，无法和外网通信（简单来讲就是你连百度都百度不了，只能和主机之间传递数据）
```

网关

```
网关 = 你这个局域网，通往外面世界的“出口大门”

局域网内的所有设备，不能直接访问互联网，必须经过统一的大门才能出去,就是网关

网关到底干了啥？
1.跨网段通信
	把内网数据包发到外网，把外网数据带回给你
2.通常就是你的路由器
3.网关≠路由器，但家用里基本是同一个


自己的理解：
从协议上看，网关是一个局域网ip地址。
从设备上看，网关是一台真实的设备，拥有局域网内的一个ip地址
所以网关必须占用局域网内的一个ip地址
```



设置静态IP，方便主机远程连接到虚拟机

```
修改配置文件
/etc/sysconfig/network-scripts/ifcfg-ens33
生效
systemctl restart network
```

![image-20260307210939328](C:\Users\95239\AppData\Roaming\Typora\typora-user-images\image-20260307210939328.png)

配置主机名

```
修改主机配置文件
/etc/hostname
生效
要么重启服务器，要么如下操作
hostnamectl set-hostname 修改的名

要有一张主机名与ip的映射表（hosts文件）
/etc/hosts
```

## 1.4 远程登录

最简单的方式就是 ssh

```
windows命令行
ssh 用户名@主机名
```

![image-20260307213517935](C:\Users\95239\AppData\Roaming\Typora\typora-user-images\image-20260307213517935.png)

以上方式简单，但功能也比较少，更多的是用三方软件，如xshell，putty等

## 1.5 系统管理

Linux中的进程和服务

```
服务是常驻的进程，可以理解为守护进程

进程与守护进程
守护进程其实就是一种特殊的进程
```

centos 6之前的旧命令，service

新命令，systemctl

```
systemctl start|stop|restart|status 服务名

查看服务的方法
/usr/lib/systemd/system
```

关闭centos 6的network,只保留centos 7的NetworkManager

```
systemctl stop network
systemctl restart NetworkManager
```



配置服务的开机自启动选项

```
setup
有*的代表开机自启动，通过移动光标然后，然后用空格进行切换启动状态
```

![image-20260307220244467](C:\Users\95239\AppData\Roaming\Typora\typora-user-images\image-20260307220244467.png)

关于运行级别

```
运行级别是几，开机时就只会启动对应的那些服务
```

![image-20260308131531164](E:\Note\linux的学习.assets\image-20260308131531164.png)

![image-20260308131641532](E:\Note\linux的学习.assets\image-20260308131641532.png)

```
查看当前运行级别
systemctl get-default

/etc/inittab

切换运行级别
init 3
```

配置服务开机自启与防火墙相关

```
systemctl enable/disable 服务名

systemctl disable firewalld
```

关机命令

```
立刻关机（最标准，最安全）shutdown -h now
10分钟后自动关机shutdown -h 10
具体时间关机shutdown -h 20:30
立刻关机poweroff等价shutdown -h now
停止系统，可能需要手动断电halt
```

重启命令

```
立刻重启reboot
立刻重启shutdown -r now
```

# 2.实操篇

## 2.1 前言

以下内容掌握了，会方便今后自己学习陌生命令

* 帮助命令

```
man [命令或配置文件] (man----manual手册)

进入后翻页
f、b、空格
```

+ help获得shell内置命令的帮助信息

```
help 命令

判断一个命令是内部还是外部命令	type 命令
```

* 或者通过 [命令] --help的方式

其他命令

```
清屏
Ctrl+l
clear
reset
```



## 2.2 文件目录类

命令大全

```
pwd
ls
cd
mkdir
rmdir
touch
cp
rm
mv
cat
more
less
echo
>输出重定向和>>追加
ln软链接
head
tail
```

## 2.3 时间日期类

```
date显示当前时间
```

![image-20260308135946207](E:\Note\linux的学习.assets\image-20260308135946207.png)

## 2.4 用户管理类

添加新用户

```
useradd 用户名
useradd -g 组名 用户名		添加新用户到某个组

产看用户
id 用户名

whoami与who am i
```

设置用户密码

```
password 用户名
```

查看配置文件创建了哪些用户

```
/etc/passwd
```

设置普通用户具有root权限

```
sudo

/etc/sudoers
```

删除用户

```
userdel 用户名

以此种方式只会删除用户，用户的相关信息（主目录）会保留
```

用户组管理

```
/etc/group

新增组 groupadd 组名
```

## 2.5 搜索查找类

1.查找文件或者目录

* find

```
find 指令将从指定目录向下递归地遍历其各个子目录，将满足条件的文件显示在终端

find [搜索范围] [选项]

[选项]
-name
-user
-size
```

* locate

```
快速定位文件路径
locate指令利用事先建立的系统中所有文件名称及路径的locate数据库实现快速定位给定的文件。locate指令无需遍历整个文件系统，查询速度较快。为了保证查询结果的准确度，管理员必须定期更新locate时刻

locate 搜索文件

由于locate指令基于数据库进行查询，所以第一次运行前，必须使用updatedb指令创建locate数据库
```

* grep

```
grep 选项 查找内容 源文件
-n	显示匹配行及行号
```

## 2.6 压缩/解压类

* gzip/gunzip

```
gzip	只能压缩文件，*.gz

只能压缩文件不能压缩目录
不保留原来的文件
同时多个文件会产生多个压缩包
```

* zip/unzip
* tar

```
tar打包
tar [选项] XXX.tar.gz 将要打包进去的内容

[选项]
-c	产生.tar打包文件
-v	显示详情信息
-f	指定压缩后的文件名
-z	打包同时压缩
-x	解包.tar文件
-C	解压到指定目录
```





# 3.扩展篇

## 3.1 shell编程

1.shell脚本入门

```
脚本的第一行都是指定bash的解析器
#!/bin/bash

执行方式
①bash 脚本的路径
②./脚本
```

shell和子shell

ps -f



2.变量

* 系统变量
  * $HOME
  * $PWD
  * $SHELL
  * $USER

```
查看系统变量的值
echo $HOME

env查看所有系统全局变量

set查看所有变量
```

* 用户变量

```
基本语法
定义变量	变量名=变量值
撤销变量	unset 变量名

全局变量的创建方法：先创建，再export 变量名
只读变量的创建方法：readonly 变量名=变量值
```

* 特殊变量

接收参数

```
$n	n:1-9

$#	获取所有参数个数

$*	获取所有参数，并将其当成一个整体
$@	获取所有参数，并把每个参数单独看待

$？	最后一次执行的命令的返回状态
```



3.运算符

```
expr 1 + 2

基本语法
$((运算式))或者$[yun'suan]
```



4.条件判断

```
test condition
[ condition ]	condition前后必须有空格

常用判断条件
-eq
-lt
-gt
!=

文件权限的判断
-r 文件
-w
-x

按文件类型进行判断
-e 文件	#是否存在该文件
-f file	  #是否是文件
-d dir		#是否是目录

多条件判断
condition1 || condition2	1真则2不执行	
condition1 && condition2	1真则2才执行

```



5.流程控制

* if判断

```
单分支
if [ 条件判断式 ];then
	程序
fi

if [ 条件判断式 ]
then
	程序
fi

多分支
if [ 条件判断式 ]
then
	程序
elif [ 条件判断式 ]
then
	程序
else
	程序
fi
```

* case语句

```
case $变量名 in
"值1")
	程序
;;
"值2")
	程序
;;
*)
	如果均不是，则执行此处
;;
esac
```

* for循环

```
for (( 初始值;循环控制条件;变量变化 ))
do
	程序
done

for 变量 in 值1 值2 值3...
do
	程序
done
```

* while循环

```
while [ 条件判断式 ]
do
	程序
done
```



* read读取控制台输入

```
read (选项) (参数)

选项
	-p	指定读取值时的提示符
	-t	指定读取值时等待的时间(秒)
参数
	即变量
```



6.函数

* 系统函数

```
basename [string/pathname] [suffix]

dirname [string]
```

* 自定义函数

```
[ function ] funname[()]
{
	Action
	[return int]
}

```



## 3.2 软件包管理

1.RPM

```
rpm -qa		查询所有安装的rpm包
rpm -qi 软件包		查询该软件包的具体信息

-e 卸载
--nodeps 卸载时不检查依赖
rpm -e RPM软件包
rpm -e --nodeps 软件包

安装
-i	install
-v	--verbose显示详细信息
-h	--hash进度条
--nodeps	安装前不检查依赖
rpm -ivh RPM包全名
```

2.YUM

```
yum [选项] [参数]

[选项]
-y	自动yes

[参数]
install
update
check-update
remove
llist
clean
deplist

修改YUM源
/etc/yum.repos.d/Centos-Base.repo

yum install wget
cp /etc/yum.repos.d/Centos-Base.repo /etc/yum.repos.d/Centos-Base.repo.backup
wget http://mirrors.aliyun.com/repo/Centos-7.repo
```

## 3.3 克隆虚拟机





