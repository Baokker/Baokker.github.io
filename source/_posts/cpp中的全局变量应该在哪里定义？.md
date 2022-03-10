---
title: cpp中的全局变量应该在哪里定义？
author: Baokker
avatar: 'https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/img/custom/avatar.jpg'
authorLink: https://Baokker.github.io
categories: 技术
comments: true
photos: 'https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/defaultImages.jpg'
date: 2022-01-18 17:02:51
tags:
 - 全局变量
keywords: 全局变量
description: 写五子棋遇到的问题..
---



真正发现这个问题，是在写五子棋的时候，想在.h中设一个全局变量表示难度`difficulty`，然后在.cpp中修改`difficulty`，结果发现报了错。查阅后发现是重定义的问题。在.h中定义了`difficulty`，再在多个cpp里修改的时候，compiler就不知道用哪个了，然后就是经典的LNK2019（杀气重重



最后还是选择**在h中声明，在一个制定的cpp中定义**。这样避免了二义性



总之，假设工程中的多个源文件需要这个全局变量，那么，就任找一个a.h头文件，用extern去**声明**这个变量,然后源文件a.cpp中去**定义**它（注意，这个是真正定义的地方,不再需要带extern），最后在需要使用这个全局变量的源文件中`include"a.h"`就OK了（其他的cpp中为了程序的可读性, 最好还是加上extern声明）



例子:https://blog.csdn.net/MrZhangXX/article/details/84109902



