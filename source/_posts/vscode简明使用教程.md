---
title: vscode简明使用教程
author: Baokker
avatar: 'https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/img/custom/avatar.jpg'
authorLink: 'https://Baokker.github.io'
categories: 技术
comments: true
photos: >-
  https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/pexels-picjumbocom-461077.jpg
date: 2022-03-27 10:38:51
keywords:
description:
---




# 参考链接

https://blog.csdn.net/maokelong95/article/details/88805589



# 安装

进入[官方下载页面](https://code.visualstudio.com/download)，根据不同的系统下载对应的安装包即可。例如，如果使用Ubuntu/Debian，就下载.deb，如果使用CentOS，RHEL之类，就下载.rpm



# 汉化

> 按下“Ctrl+Shift+P”组合键以显示“命令面板”，然后键入“display”以筛选并显示“Configure Display Language”命令。按“Enter”，然后会按区域设置显示安装的语言列表，并突出显示当前语言设置。



# 快捷键

| 快捷键                  | 功能                                          |
| ----------------------- | --------------------------------------------- |
| `Ctrl + Shift + P`,`F1` | 打开设置                                      |
| `Ctrl + c`              | 复制行                                        |
| `Ctrl + x`              | 剪贴行                                        |
| `Alt + ↑/↓`             | 将光标所在的该行上/下移动                     |
| `Ctrl + Shift + K`      | 删除整行（`dd` in vim）                       |
| `Ctrl + /`              | 注释（大部分代码支持）                        |
| `Ctrl + ]`,`Ctrl + [`   | 向右/左缩进                                   |
| `Ctrl + home/end`       | 跳转到该文件最开始/最末尾                     |
| `Ctrl + K + F`          | 自动排版                                      |
| `Ctrl + F/H`            | 查找/替换                                     |
| `Ctrl + Shift + F / H`  | 在该工作区内查找/替换                         |
| `F3`,`Shift + F3`       | 查找后向前/向后跳转结果                       |
| `Ctrl + 1/2/3..`        | 打开多个窗口时，迅速切换到第n个窗口，类似tmux |

link: https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf



# 配置，运行，和debug

在这里仅展示Linux系统（Ubuntu为例）下的配置，因为..Windows下配置反而麻烦很多..

## c/c++

先安装好编译器和debugger：

```bash
sudo apt-get update
sudo apt-get install build-essential gdb # 安装gcc g++ gdb
```

确保安装：

```bash
gcc -v
```

再在插件里安装两个插件，一个是vscode一开始就推荐安装的`C/C++`，还有一个是`Code Runner`：

![](https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/20220326115003.png)

![](https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/20220326115032.png)

安装完code runner后，右上角都会出现一个运行的箭头标志，按下即可开始运行。

![](https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/20220326115235.png)

## Python

直接下载Python扩展即可



# Java

待更新..



---

**[Pexels](https://www.pexels.com/zh-cn/photo/461077/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)** 上的 **[picjumbo.com](https://www.pexels.com/zh-cn/@picjumbo-com-55570?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)** 拍摄的图片