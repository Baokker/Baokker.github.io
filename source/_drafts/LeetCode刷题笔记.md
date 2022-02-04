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
