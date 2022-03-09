---
title: LeetCode刷题笔记
categories: 技术
photos: 'https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/defaultImages.jpg'
---



## 707 设计链表

单链表有头结点，同样地，在双链表中，除了虚拟的头结点之外，**还要再添加一个虚拟的尾结点！！**



## 24

做链表时尤其应当意识到手动画图，草稿的重要性..



# 19

经典快慢双指针

另外

```cpp
        while (i < n){
            fast = fast->next;
            i++;// always forget!
        }
```

always forget!!



# 哈希表

哈希碰撞：计算出的哈希编码相同

拉链法：构成链表

线性探测法：放在原来的后面一位



unordered_set vs unordered_map



# 242

区分`for (char c : s)`和`for (char &c : s)`：前者会将原先的s字符串再拷贝一遍，后者则直接引用。因此前者花费的世界会比后者多。



# stack and queue

栈的内部结构，栈的底层实现可以是vector，deque，list 都是可以的， 主要就是数组和链表的底层实现。

**我们常用的SGI STL，如果没有指定底层实现的话，默认是以deque为缺省情况下栈的低层结构。**

我们也可以指定vector为栈的底层实现，初始化语句如下：

```text
std::stack<int, std::vector<int> > third;  // 使用vector为底层容器的栈
```



# 232

再多说一些代码开发上的习惯问题，在工业级别代码开发中，最忌讳的就是 实现一个类似的函数，直接把代码粘过来改一改就完事了。

这样的项目代码会越来越乱，**一定要懂得复用，功能相近的函数要抽象出来，不要大量的复制粘贴，很容易出问题！（踩过坑的人自然懂）**



# 1047

而且**在企业项目开发中，尽量不要使用递归！**在项目比较大的时候，由于参数多，全局变量等等，使用递归很容易判断不充分return的条件，非常容易无限递归（或者递归层级过深），**造成栈溢出错误（这种问题还不好排查！）**
