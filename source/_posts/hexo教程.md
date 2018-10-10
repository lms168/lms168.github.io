---
title: hexo的使用
description: 学习下hexo的书写
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
