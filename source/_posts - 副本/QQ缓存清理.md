---
title: QQ缓存清理
author: Baokker
avatar: 'https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/img/custom/avatar.jpg'
authorLink: Baokker.github.io
categories: 技术
comments: true
photos: 'https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/pexels-francesco-ungaro-3172277.jpg'
date: 2022-01-18 17:37:28
keywords: 缓存
description: 我的评价是不如电报（bushi
---



刚从32G的手机换到128G的时候，觉得手机的内存那么大，怎么都不会用完。想不到过了一年半，已经是每天都为几GB剩余空间和垃圾斗得你死我活..（什么，我竟然曾经装下过原神？）

发现自己QQ的空间有20G，微信有8G，真的想不通，国内的软件个个1G起步，装下的国外软件，个个界面简洁，体验舒适，大小一般半个G就够了，真的很不理解多出来那么多哪里的垃圾..

于是狠狠研究了一番，得出的最终结论是：qq和微信在Android系统里，会对以前的（99.99%没有用处）的图片等进行缓存，具体位置为：
（qq，以前的大量缓存图片）
**/storage/emulate/0/Android/data/com.tencent.mobileqq/Tencent/MobileQQ/chatpic**
（wechat，不过这是以前的聊天记录）
**/storage/emulate/0/Android/data/com.tencent.mm/MicroMsg**

一狠心删掉了8G的chatpic和2G的MicroMsg
