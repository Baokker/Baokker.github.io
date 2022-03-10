---
title: Linux运行数据结构课设感想
author: Baokker
avatar: 'https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/img/custom/avatar.jpg'
authorLink: Baokker.github.io
comments: true
categories: 技术
photos: 'https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/defaultImages.jpg'
date: 2022-01-21 19:54:12
keywords: centos Makefile
description: 唉 卷不动啊
tags: 
- 技术
---

数据结构课设加分项，使代码能够在linux下使用G++编译通过，并上传makefile。

## VMware安装

难度不大，去官网[下载](https://www.vmware.com/cn/products/workstation-pro/workstation-pro-evaluation.html)，然后找个pojiema即可。记得安装软件和虚拟机的时候要注意C盘的剩余空间，最好还是分装在别的系统盘上。

## CentOS安装

可参考这个[链接](https://blog.csdn.net/m0_46855648/article/details/111365163)

建议安装时先选择最小安装（minimum install），之后加上图形化：

```bash
yum groupinstall "Server with GUI" -y # install
systemctl set-default graphical # set GUI interface as default
```

## 安装g++

先是安装：

```bash
sudo dnf group install "Development Tools" # gcc g++ make,etc will be installed
sudo dnf install man-pages # optional for manual pages
```

之后可以对文件编译。可以通过与主机文件传输，也可以直接在Linux里编写（这样的话，另外需要学一点vim的知识）

```bash
g++ -o output_file_name input_file.cpp
```

其中`output_file_name`是一个可执行文件，直接在shell里运行`./output_file_name`即可。

## 与主机文件共享

这个难关非常难啃，我捣腾了非常久..也没解决。

最后得出的解决方案是，每次在开机时，都要先输入如下指令：

```bash
sudo vmhgfs-fuse .host:/ /mnt/hgfs -o subtype=vmhgfs-fuse,allow_other
```

这样，在`/mnt/hgfs/`中会显示共享文件夹。（暂时没能实现开机自动挂载，知识还是太浅薄了）

## 字符编码

一开始直接将VS下的cpp传入centos用g++编译，结果报了错。debug后发现是编码的问题。VS里默认的是GB2312编码（并且不支持UTF-8，而只能支持UTF-8 with BOM，很离谱），而g++默认为UTF-8。可以选择转换编码，也可以在编译时加入新的选项。

最后的选择是把所有cpp都使用notepad++转为了UTF-8 with BOM格式。

## code debug

- > free(): double free detected in tcache 2
  > Aborted (core dumped)
  
  这个bug我遇着了两回，全都被VS强大的编译防过去了（）
  
  核心在于new完的变量被delete了多回

- .hpp是.h和.cpp的结合，即将声明和定义包括在一个文件中，从而使得文件更加清晰。个人认为这样尤其有利于含template的函数，因为template的声明和定义最好放在一起，找不到定义的话就会报错。

## linux相关操作新得

- vim不保存退出:`Esc`回到normal模式，然后输入`:q!`

- cd
    1. To navigate into the root directory, use "cd /"
    2. To navigate to your home directory, use "cd" or "cd ~"
    3. To navigate up one directory level, use "cd .."
    4. To navigate to the previous directory (or back), use "cd -"
    
- vim

    - :w 保存文件但不退出vi
    - :w file 将修改另外保存到file中，不退出vi
    - :w! 强制保存，不推出vi
    - :wq 保存文件并退出vi
    - :wq! 强制保存文件，并退出vi
    - q: 不保存文件，退出vi
    - :q! 不保存文件，强制退出vi
    - :e! 放弃所有修改，从上次保存文件开始再编辑

    

## VS的编码特性

在release的文件夹里找到了`.pdb`之类的文件，查阅后发现是VS的数据文件

## make makefile cmake

只简单地阐述一下关系：make通过makefile来对指定的文件进行编码等操作，生成可执行文件；cmake则是另外一套语法，用于生成Makefile。具体教程不阐述了，我觉得我也只是学个皮毛。

