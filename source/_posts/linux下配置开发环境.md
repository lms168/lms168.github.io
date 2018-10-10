---
title: linux下开发环境配置
description: linux下开发环境配置
toc: true
categories:
- 环境搭建
tags:
- java 
- linux
---

# 配置jdk环境

下载jdk，解压到/usr/local下面
## 编辑/etc/profile,并将java的环境写入
```bash
export USR_DIR=/usr/local
export JAVA_HOME=$USR_DIR/jdk1.8.0_151
export PATH=$PATH:$JAVA_HOME/bin
```
## 执行source命令使环境变量生效
```bash
source /etc/profile
```
## 检查jdk环境是否生效
```bash
java -version
```
如果出现版本信息，则说明jdk环境ok


# 配置maven

整个安装配置的过程和jdk差不多，唯一不同的是
配置完成之后需要把安装包中的settings.xml复制到*~/.m2/*下面,然后修改settings.xml中*nexus私库*和*本地仓库localRepository*路径

# 配置svn

## 安装
```bash
sudo apt-get install subversion
```
## svn常用命令

### 创建svn目录
```bash
svn mkdir -m "创建一个文件夹"  http://192.168.0.x:18080/svn/xxx
```

### 创建svn分支
```bash
svn cp -m "创建braches下分支" http://192.168.0.x:18080/svn/xxx http://192.168.0.x:18080/svn/branches/
```
### 剪切svn分支
```bash
svn checkout http://192.168.0.x:18080/svn/xxx
```
### 添加新文件
```bash
svn add test.java
```
### 提交修改的文件
```bash
svn commit test.java -m "向项目中添加类test.java"
```
### 更新文件
```bash
svn update ./
```

# 配置git

## 安装
```bash
sudo apt-get install git
```
## 配置免密码推送到远程仓库
1. 登录远程仓库web页面，点击右上角的settings，然后点击左边SSH Keys

2. 将本地的公钥复制填入key框中保存

## 命令手册
具体使用请参看[廖雪峰老师git](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)的博客


## 一台电脑配置多个git远程仓库
1. 编辑~/.ssh/config文件，填写两个git远程仓库的信息，注意要生成两对密钥公钥 参看{% post_link ssh免密码登录 ssh免密钥登录 %}
```bash
# 配置GitLab，公司账号1：
Host att_gitlab
        HostName 192.168.0.x
        Port 22
        User lims@xxxx.com
        PreferredAuthentications publickey
        IdentityFile ~/.ssh/gitlab_zzcm_att_rsa

# 配置GitHub
Host github
        HostName github.com
        User xxx@qq.com
        IdentityFile ~/.ssh/github_rsa
```
2. 如果配置了git config --global user.name/user.mail 的全局信息则取消该全局信息,其他的使用与单git远程仓库没有区别
