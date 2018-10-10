---
title: linux常用的搜索替换命令
description: linux常用的搜索替换命令
toc: true
categories:
- 开发
tags: 
- linux
---

# 搜索

## 文件夹下包含某个字段的所有文件
```bash
在当前目录开始递归查找所有扩展名为.txt的文本文件，并找出包含”thermcontact”的行
find . -name "*.txt" | xargs grep "thermcontact"
```
## grep显示匹配前后几行信息
```bash
grep -C 5 foo file 显示file文件里匹配foo字串那行以及上下5行
grep -B 5 foo file 显示foo及前5行
grep -A 5 foo file 显示foo及后5行
```

# 替换

## vim下对所有的行添加逗号和shell的换行符（\）
```bash
g/$/s//,\\/g

替换前:
105132
106167
106349
106546
106569

替换后
105132,\
106167,\
106349,\
106546,\
106569,\
,\

```