---
title: hexo的使用
description: hexo初接触
toc: true
categories:
- 环境搭建
tags:
- hexo
---
Welcome to [Hexo](https://hexo.io/zh-cn/docs/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### config git
编辑hexo安装路径下的配置文件`_config.xml`，修改博客的github项目路径 
```bash
deploy:
  type: git
  repo: git@github.com:lms168/lms168.github.io.git
  branch: master
```

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)


## 多台电脑使用Ｈexo

### 原理
要使多台电脑使用hexo必须得明白两件事情:
1. 我们使用`hexo d`命令推送生成的静态文章，实际上推送的是`.deploy_git`目录下面的内容,与hexo安装目录下的其他文件无关
2. 如果想多台电脑使用Ｈexo， 那么就得保证多台电脑Ｈexo运行环境一样，最重要的是要保证编辑的文章`source/_posts/`在多个环境中保持同步


### 方式
理解了原理之后，要保证多台电脑使用Hexo就很简单了,以下几个方式都可以
1. 最原始的方式:u盘/网盘拷贝，每次修改了`source/_posts/`后，把该目录拷贝到u盘/网盘中，然后在另一个环境中的时候覆盖,这种方式有效但是很麻烦
2. 为`source/_posts/`在git上面单独建立一个仓库，每次写完文章后，直接推送文章，然后在另一个环境中pull，很显然这种方式便捷实用。

### 将Ｈexo环境同步到Ｇit仓库
我们可以单独为Ｈexo的环境建立一个Git仓库，但是这样子git上面就会有博客仓库与Hexo环境仓库，很不雅观。比较好的方式是，*在原先的博客仓库中创建一个分支，然后将Ｈexo环境推送到该分支*,这样子一个仓库就囊括了博客与hexo源文件，方便以后维护管理


1. 在本地初始化source分支,并且推送到博客仓库
```bash
   cd $HEXO_HOME
   git init
   git remote add origin git@github.com:lms168/lms168.github.io.git
   git checkout -b source
   git add .
   git commit ./ -m "初始化hexo运行环境"
   git push
```

2. 此时进入github的web页面可以看到博客仓库多了一个`source`的分支,然后把该分支设置为*default branch*

3. 在其他环境中`clone`该博客,然后 `npm install` 安装hexo的运行环境

4. 每次修改了`source/_posts/`后要`git push`，　每次开始写日志之前要 `git pull`;保证日志文件在各个环境中保持同步










































