---
title: 为什么变量名称前有k？
categories: 随想
index_img: 'https://baokker-oss-blog-hangzhou.oss-cn-hangzhou.aliyuncs.com/cdn_for_blog/blog_imgs/defaultImages.jpg'
banner_img: 'https://baokker-oss-blog-hangzhou.oss-cn-hangzhou.aliyuncs.com/cdn_for_blog/blog_imgs/defaultImages.jpg'
date: 2022-01-17 00:17:26
tags: 编程
excerpt: const
---





> 这是习惯的原因。在以前的很多编程命名规范中，c代表char，一般不用c来做前缀指示常量；德语中konstant是常量的意思，同时数学上也经常用k来代表常量，因此常用k来做常量的前缀指示。从google的c++编程规范中，也有这样的建议，用k来做前缀，用作常量的前缀。
> 作者：Jim Zhou
> 链接：https://www.zhihu.com/question/39841351/answer/186178734
> 来源：知乎
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

简单来说，例如`kBoardSize`,`kPointLength`等变量名中，`k`都是`c(k)onstant`的意思，用以区分变量和常量。也算是解答了读代码时的一个疑惑。
