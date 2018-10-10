---
title: linux下开发常用命令
description: linux下开发常用命令
toc: true
categories:
- 开发
tags:
- java 
- linux
---


**本文档是一个快速使用linux作为开发环境的查询手册，对于一些命令的更具体更合理的用法，可自行百度学习**


# 基本的增删改命令
## 创建文件
```bash 
touch test.txt
```
## 向文本中追加内容
```bash
echo "222" >> test.txt 
```
## 覆盖文本中的所有内容 
```bash
echo "111" > test.txt 
```
## 查看文本中的内容
```bash
cat test.txt 
```

## 创建级联目录
```bash
mkdir -p /xx/xx
```

## 文件重命名
```bash
mv test.txt test1.txt
```
---

# 开发中常用命令
## ssh命令
```bash
ssh root@centos90
```

## scp命令
+ 将本机上的文件夹传到远程服务器
```bash
scp -r /usr/local/jdk root@centos90:/usr/local
```

+ 将远程服务器上面的文件夹拉取到本机
```bash
scp -r root@centos90:/usr/local/jdk ./
```
## 查看本地端口是否被占用
```bash
lsof -i:8080
或者
netstat -tupl | grep 9902
```

## 查看远程端口是否开启
+ 端口未开启
```bash
lms@LMS:~/Blog/blog/themes/maupassant$ telnet 192.168.0.90 9092
Trying 192.168.0.90...
telnet: Unable to connect to remote host: Connection refused
```

+ 端口已启用
```bash
lms@LMS:~/Blog/blog/themes/maupassant$ telnet 192.168.0.90 9902
Trying 192.168.0.90...
Connected to 192.168.0.90.
Escape character is '^]'.
```

## head/tail显示文件内容
*-n :* 表示显示多少条
*-f :* 表示滚动显示
+ 显示文件头部信息
```bash
head -n 10 log.txt
```

+ 显示文件尾部信息
```bash
tail -n -f  10 log.txt
```

## 列出所有java进程的pid
```bash
jps
```

## ps -ef用标准的格式显示进程信息
```bash
过滤含有tomcat关键字的所有进程信息
ps -ef|grep tomcat
```


---

# 配置linux的工作环境

## 查看linux的发行版本
```bash
lsb_release -a
```

## 查看内存的使用情况
```bash
 free -m
```

## 查看cpu的情况
+ 查看cpu的个数
```bash
cat /proc/cpuinfo|grep "physical id"|uniq|wc -l
```
+ 查看cpu的核数
```bash
cat /proc/cpuinfo|grep "cpu cores"|uniq
```

+ 查看cpu的型号频率
```bash
cat /proc/cpuinfo|grep "model name"|uniq
```

## 配置ubuntu开发环境
+ 安装[搜狗输入法](https://pinyin.sogou.com/linux/?r=pinyin),并且配置*fcitx*
+ 安装[wine](https://wiki.winehq.org/Ubuntu_zhcn)
+ 安装[QQ](https://github.com/askme765cs/Wine-QQ-TIM) 本地环境有wine之后免安装即可运行

## 主机名配置
*主机名(hostname)：*在一个局域网中，每台机器都有一个主机名，用于主机与主机之间的便于区分，就可以为每台机器设置主机名，以便于以容易记忆的方法来相互访问
+ 修改ubuntu的主机名
```bash
1. 编辑 /etc/hostname,填入主机名  
    LMS
2. 编辑/etc/hosts，将主机名对应的ip映射写入该文件中  
    192.168.0.54       LMS
```
+ 修改centos6.x的主机名
```bash
1.编辑/etc/sysconfig/network，修改主机名HOSTNAME对应的值
    NETWORKING=yes
    HOSTNAME=centos92
    GATEWAY=192.168.0.1

2.编辑/etc/hosts,将主机名对应的ip映射写入该文件中  
    192.168.0.90       centos90
```
+ 修改centos7.x的主机名
```bash
1. 编辑 /etc/hostname,填入主机名  
    adx61
2. 设置主机名
    sudo hostnamectl --static set-hostname adx61
```


## 域名配置
*域名(domainname)：*通俗的理解就是ip地址的简称。每个域名都对应一个IP地址，但一个IP地址可有对应多个域名

添加/修改域名
```bash
一个ip地址对应多个域名
192.168.0.90 centos90
192.168.0.90 cccccccc
```
## 静态ip配置
实际开发中如果ip地址一直变化是无法忍受的，故我们需要配置一个静态ip地址
+ ifconfig查看ip信息
```bash
lms@LMS:~/Blog/blog$ ifconfig
enp2s0    Link encap:以太网  硬件地址 44:8a:5b:65:31:8e  
          inet 地址:192.168.0.54  广播:192.168.1.255  掩码:255.255.254.0
          inet6 地址: fe80::468a:5bff:fe65:318e/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  跃点数:1
          接收数据包:1768559 错误:0 丢弃:50576 过载:0 帧数:0
          发送数据包:273080 错误:0 丢弃:0 过载:0 载波:0
          碰撞:0 发送队列长度:1000 
          接收字节:593436184 (593.4 MB)  发送字节:40078308 (40.0 MB)

lo        Link encap:本地环回  
          inet 地址:127.0.0.1  掩码:255.0.0.0
          inet6 地址: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  跃点数:1
          接收数据包:183591 错误:0 丢弃:0 过载:0 帧数:0
          发送数据包:183591 错误:0 丢弃:0 过载:0 载波:0
          碰撞:0 发送队列长度:1000 
          接收字节:76191308 (76.1 MB)  发送字节:76191308 (76.1 MB)

```
+ 编辑文件/etc/network/interfaces配置静态ip
```bash
# interfaces(5) file used by ifup(8) and ifdown(8)
auto lo
iface lo inet loopback

# The primary network interface
auto enp2s0                 // 使用的enp2s0这个接口
iface enp2s0 inet static    // 对这个接口，使用静态ip设置 
address 192.168.0.54        // 要配置的静态ip地址
netmask 255.255.254.0       //子网掩码
gateway 192.168.0.1         //网关
#dns-nameserver 114.114.114.114  //DNS地址，可暂时不配置，待后面配置
```

+ DNS服务器配置
*一台机器可以配置多个域名解析器*

1. 编辑文件/etc/resolv.conf(机器重启被擦除)
```bash
nameserver 144.144.144.144
```
2. 编辑文件/etc/resolvconf/resolv.conf.d/base(重启不会被擦除) 
```bash
nameserver 144.144.144.144
```
+ 重启电脑或者网络，即可以愉快上网了

# 配置linux部署环境
*由于是内网故只是简单的打开关闭了防火墙，如果是正式环境应该根据实际需要开放端口*

## centos6防火墙相关命令
+ 查看防火墙状态
```bash
service iptables status
```
+ 关闭防火墙
```bash
临时生效(重启后无效):  service iptables stop
永久生效(重启后仍有效): chkconfig iptables off
```
+ 开启防火墙
```bash
临时生效(重启后无效)：service iptables start
永久生效(重启后仍有效)：chkconfig iptables on
```
## centos7防火墙相关的命令
+ 查看防火墙状态
```bash
ssh adx61 firewall-cmd --state 
```
+ 关闭防火墙
```bash
ssh adx61 systemctl stop firewalld.service
```
+ 开启防火墙
```bash
ssh adx61 systemctl start firewalld.service
```

## 创建用户和组
以创建一个运行elasticsearch程序的用户为例
1. 创建用户组es
```bash
groupadd es
```
2. 创建用户esUser并且加入到es组中
```bash
useradd esUser -g es -p zzcm2014
```

3. 修改要运行的文件的归属
```bash
chown  -R esUser:es /usr/local/elasticsearch-5.4.0
```

4. 切换为创建的用户esUser
```bash
su esUser
```

## 修改文件的执行权限
对于没有执行权限文件的最粗暴的解决方式
```bash
chmod -R 777 /xx/*
```

# 一些小技巧
## 免用户名ssh登录
修改~/.ssh/config文件，添加如下配置
```bash
Host 90
HostName 192.168.0.90
User root



Host 91
HostName 192.168.0.91
User root

Host 92
HostName 192.168.0.92
User root

```
则登录时可直接使用`ssh centos90`就可以登录了，再也不用写`ssh root@centos90`了

## 对远程机器批量执行命令
以批量启动zk服务为例
```bash
for i in {61..65}; do ssh adx$i "cd /usr/local/zookeeper-3.4.10/bin;sh  zkServer.sh start"; done
```

## vim对所有的行添加逗号和shell的换行符
```bash
g/$/s//,\\/g
```





