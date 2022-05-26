---
title: YouCompleteMe安装教程
author: Baokker
avatar: 'https://raw.githubusercontent.com/Baokker/cdn_for_blog/main/img/custom/avatar.jpg'
authorLink: https://Baokker.github.io
categories: 技术
comments: true
photos: https://raw.githubusercontent.com/Baokker/cdn_for_blog/main/blog_imgs/pexels-kaju-9444064.jpg
date: 2022-02-12 11:54:15
keywords: YCM
description: 非常好用的vim代码自动补全插件
---





按着官网和其他大佬的教程走了一回。安装确实很复杂，但，总的来说，实现linux爬梯子后很顺畅。

对了，YCM是什么？是一款针对vim的自动补全的插件，非常牛逼，堪比vs的自动补全。用tab和shift tab即可自动联想。

话不多说。

# prerequisite

首先要确保vim版本大于8.1，并且vim能支持python 3（3.6以上），可以输入`vim --version`检查



# 安装vundle

```bash
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

然后打开.vimrc（`vim ~/.vimrc`)，粘贴如下：（vim教程就不教了哈，最简单直接`i`，然后粘贴，然后`Escape`，然后`:wq`，就好了）

```text
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

" The following are examples of different formats supported.
" Keep Plugin commands between vundle#begin/end.
" plugin on GitHub repo
Plugin 'tpope/vim-fugitive'
" plugin from http://vim-scripts.org/vim/scripts.html
" Plugin 'L9'
" Git plugin not hosted on GitHub
Plugin 'git://git.wincent.com/command-t.git'
" git repos on your local machine (i.e. when working on your own plugin)
Plugin 'file:///home/gmarik/path/to/plugin'
" The sparkup vim script is in a subdirectory of this repo called vim.
" Pass the path to set the runtimepath properly.
Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}
" Install L9 and avoid a Naming conflict if you've already installed a
" different version somewhere else.
" Plugin 'ascenator/L9', {'name': 'newL9'}

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line
```

最后运行

```bash
vim +PluginInstall +qall
```



# 安装 CMake, Vim and Python

```bash
apt install build-essential cmake vim-nox python3-dev
```



# 安装 mono-complete, go, node, java and npm

```bash
apt install mono-complete golang nodejs default-jdk npm
```



# 下载源码，获取相关依赖

```bash
# 这两步因为网速会非常慢，建议先实现科学上网
# 获取源码
git clone https://github.com/ycm-core/YouCompleteMe ~/.vim/bundle/YouCompleteMe 

# 解决相关依赖
cd ~/.vim/bundle/YouCompleteMe
git submodule update --init --recursive 
```



# 安装

```bash
~/.vim/bundle/YouCompleteMe$ python3 install.py --clangd-completer # 对c/cpp自动补全，可以改成--all，支持所有语言
```



差不多好了！~

![](https://raw.githubusercontent.com/Baokker/cdn_for_blog/main/blog_imgs/20220212115145.png)

