---
title: nginx常用命令
description: nginx常用命令
toc: true
categories:
- 开发
tags: 
- linux
---

# nginx常用命令

## 启动nginx服务
```bash
nginx -c /usr/local/nginx/conf/nginx.conf
```

## 查看nginx运行状态
```bash
ps -ef|grep nginx
root     31064     1  0 15:59 ?        00:00:00 nginx: master process ./sbin/nginx -c ./conf/nginx.conf
```

## 检测nginx.conf是否正确
```bash
nginx -t
```

## 重新加载修改后的nginx的配置文件
```bash
nginx -s reload
```

## nginx帮助文档
```bash
nginx -h
```