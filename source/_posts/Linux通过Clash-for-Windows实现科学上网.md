---
title: Linux通过Clash for Windows实现科学上网
author: Baokker
avatar: 'https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/img/custom/avatar.jpg'
authorLink: https://Baokker.github.io
categories: 技术
comments: true
photos: https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/pexels-yuliya-kosolapova-11066975.jpg
date: 2022-02-12 11:54:24
keywords: Linux
description: 实现的那一刻很开心！
---





# 起因

花了三四天的时间才总算迷迷糊糊地搞出了这个问题。为什么一定这么执着呢？

1. 最近在学习[a missing semester](https://www.youtube.com/playlist?list=PLyzOVJj3bHQuloKGG59rS43e29ro7I57J)这个课程，也学着运行Linux下的一些命令。
2. 遇到的两个非常严重的问题，一是在Windows上用YouTube观看course，再在虚拟机上的Ubuntu实操，来回切换很累，手一直要去拿鼠标；二是在git clone时，下载很慢，严重影响了学习的心情和效率。

因此，捣腾了好几天，并且卡了好几天bug，总算是搞出了Ubuntu20.04下的Clash梯子。方法还算简便，但是我也不知道为什么捣腾了很久（）在此记录一下



# 过程

总体可参考这个[链接](https://www.youtube.com/watch?v=VOlWdNZAq_o)（额，不过是油管的）

1. 前往https://github.com/Fndroid/clash_for_windows_pkg/releases下载最新版Clash for Windows的Linux安装包。clash是著名的代理软件，Clash for Windows是它的一个图形化客户端，在各大运行系统中都可以运行，不仅限于Windows（起名很有误导性）。
   ![](https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/20220212101855.png)

2. 移动安装包到Ubuntu下，到你选定的安装位置下并解压。例如我将其放在`Work`文件夹中：

   ```bash
   mkdir ~/Work
   cp Clash..tar.gz ~/Work # 省略版本名
   tar -zxvf Clash..tar.gz # 解压
   mv Clash.... Clash # 简短名字
   cd Clash
   ```

   （写作过程中发现，可以在搜狗输入法中调整标点设置，这样可以在中文状态下直接按`（1左边的那个键）即可实现代码块包裹，生产力大幅提升！）

3. 移动到文件夹中，运行`./cfw`，即可打开客户端：
   ![](https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/20220212103848.png)
   ![](https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/20220212104353.png)

4. 找到你的梯子订阅地址（我是用的bywave，选择第二个订阅链接）（这里注意，有些订阅链接可能需要clash不能识别，需要转换）

   ![](https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/20220212104712.png)

   （上图这个一键导入clash仅限于Windows（））
   然后转入clash的Profiles，粘贴后Download，左侧有绿标说明下载成功并且已经应用。
   ![](https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/20220212104848.png)

5. 接下来是修改设置使clash能够代理，我在这里卡了很久，并且也不知道最后是怎么好的，就都记录一下吧。

6. 修改系统设置。打开设置，选择`Network`，进行如下修改，使其端口与clash端口对应
   ![](https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/20220305233146.png)
   理论上，到这里就已经OK了，而且我用chrome也是直接就能翻墙了，但是之前用Firefox一直都不行。de了好久，发现在浏览器这边出了问题。

7. 修改Firefox设置，使clash能对浏览器代理（后证明，在完成6后，使用系统代理设置也可翻墙）：
   ![](https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/20220212112647.png)
   写到这里应该懂了，Firefox一开始可能是前两个选项，所以我一直都进不去，而chrome一开始就选择使用系统代理配置，所以直接就可以访问外网了，而Firefox还要再加手动配置。



至此，总算是实现Ubuntu翻墙自由啦！之前下载YouCompleteMe的网速问题也马上迎刃而解，很舒服。
