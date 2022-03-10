---
title: tmux自定义配置一览
author: Baokker
avatar: 'https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/img/custom/avatar.jpg'
authorLink: https://Baokker.github.io
categories: 技术
comments: true
photos: 'https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/dog-5146351_1920.jpg'
date: 2022-03-04 10:27:23
keywords: tmux
description: 修改prefix，增加体验舒适度
---




[tmux](https://phoenixnap.com/kb/tmux-tutorial-install-commands)在linux系统中用于处理多窗口的命令行非常方便，然而学习后发现，默认的`Ctrl+b`前缀（prefix）快捷键已经足够反人类了，没想到还要用例如`%`的符号来划分pane，实在是离谱得很，所幸后来在网上找到了自定义配置文件的教程，修改配置后操作起来顺手多啦~

（参考链接：https://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/）

（顺带提个使用经验，tmux里选择文本时都必须先按住`shift`键，例如你想复制粘贴时，就必须一直按着`shift`，蛮离谱的也）

1. 打开命令行，`touch ~/.tmux.conf`，建立tmux配置文件
2. `vim ~/.tmux.conf`，然后粘贴以下内容

```bash
# 原先的C-b太反人类了，修改prefix为C-a
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix

# 原先用"和%来纵向/横向分割，实在是太难记住了，修改为|和-，表示纵向和横向
# 例如，想纵向分割，就只需要Ctrl+a+|即可
bind | split-window -h
bind - split-window -v
unbind '"'
unbind %

# reload config file (change file location to your the tmux.conf you want to use)
bind r source-file ~/.tmux.conf

# 原来在不同pane之间切换也很麻烦，改成alt + 上下左右 好记了很多
# switch panes using Alt-arrow without prefix
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U                                                 
bind -n M-Down select-pane -D
 
# Enable mouse mode (tmux 2.1 and above)
set -g mouse on
```

保存后退出

3. `sudo reboot`

这个时候再打开tmux就可以用自己的configuration啦~
