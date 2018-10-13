---
title: git的使用
toc: true
date: 2018-10-13 17:16:44
description: git的使用
categories:
- 工具
tags: 
- git
---

# git的工作原理
先来张git的工作原理图
![图1](/images/git1.png "图片1")

1. git本质上就是一个*key-value*数据库
2. 每次`git add`操作就是针对每一个暂存的文件在`.git/objects/`生成一个记录文件,并且返回一个hash码
3. 每次`git commit`就是把之前`git add`产生的所有的hash码还有提交的备注信息进行汇总，并且在`.git/objects/`下面生成一个记录文件，并且返回hash码；*该hash码就是commitId*
   
# git命令示意图
![图2](/images/git2.jpg "图片2")
