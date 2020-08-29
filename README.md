---
title: Hello fish shell # 这是标题
author: chempeng
date: '2018-08-08'
categories:  # 这里写的分类会自动汇集到 categories 页面上，分类可以多级
- Tool # 一级分类
tags:   # 这里写的标签会自动汇集到 tags 页面上
- 工具 # 可配置多个标签，注意格式
---

Finally, a command line shell for the 90s.

<!--more-->

什么是 fish shell ？ 为什么用它？ 可以参考 [Fish shell 入门教程](http://www.ruanyifeng.com/blog/2017/05/fish_shell.html) 和 [量化计算中的技巧（一）](https://zhuanlan.zhihu.com/p/27816701) 。

本文记录非 root 用户在无网络连接的服务器上安装 fish shell 及环境变量的配置。

### 1. 安装

[官网](https://fishshell.com/)下载源码，解压安装。以 fish-2.4.0.tar.gz 为例，系统 CentOS 6.4。

```
tar -zvxf fish-2.4.0.tar.gz
cd fish-2.4.0
./configure --prefix=/home/username/opt/fish
make
make install
```

若想登陆即使用 fish，在 `.bash_profile` 中添加

```
exec /home/username/opt/fish/bin/fish -l
```

### 2. 环境配置

不同于 bash 在 `.bashrc` 中修改环境变量，fish 需要在 `~/.config/fish/config.fish` 中修改。（如果可以使用图形界面，使用 `fish_config` 命令可打开 Web 界面进行配置。）同时注意其语法也稍有不同，下面有几条示例。

```
set -x LD_LIBRARY_PATH /opt/intel/icc/composer_xe_2013.3.163/mkl/lib/intel64/:$LD_LIBRARY_PATH
set -x LD_LIBRARY_PATH /opt/intel/icc/composer_xe_2013.3.163/compiler/lib/intel64/:$LD_LIBRARY_PATH
set PATH $PATH /home/username/anaconda3/bin
set PATH $PATH /home/username/bin
abbr q20 "nohup mpirun -np 20 vasp </dev/null> out &"
alias l "ll -h"
alias c "cd ..; and l"
alias cc "cd ../..; and l"
```

fish 的体验感很棒，尤其对于一些简单繁琐的操作来说，相比它所提升的效率，一些小问题是可以接受和值得折腾的，实在兼容不好就退出呗，也很方便。

它还有个插件，[oh my fish](https://github.com/oh-my-fish/oh-my-fish) ， 目前还没有用它的需要，fish 开箱即用~

