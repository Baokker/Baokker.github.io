---
title: 给blog增加了LiveRe评论插件
categories: 技术
index_img: https://baokker-oss-blog-hangzhou.oss-cn-hangzhou.aliyuncs.com/cdn_for_blog/blog_imgs/rocket-ship-6489876_1920.jpg
banner_img: https://baokker-oss-blog-hangzhou.oss-cn-hangzhou.aliyuncs.com/cdn_for_blog/blog_imgs/rocket-ship-6489876_1920.jpg
date: 2022-03-13 16:30:16
excerpt: 可以给我的blog自由评论了！~
---




之前一直用[Sakura](https://github.com/honjun/hexo-theme-sakura)主题里自带的Valine评论插件来作为评论的模拟，结果发现缺点不少：

- 加载不稳定，前些天直接加载不出来

- 在国内被墙了，而且我在官方上看到了如是的信息：

  > lncld.net 域名被禁
  >
  > 2月8日
  >
  > 2022 年 1 月 27 日开始，华北节点的 lncld.net 共享域名被域名注册商停止解析（clientHold）。目前我们正努力尝试联系有关方面，争取恢复 lncld.net 的解析，但情况不是很乐观，所以 受此影响的少部分使用旧版 SDK 且未使用自定义域名的应用，还请尽快更新客户端代码，使用自定义域名。
  > [查看详情 ](https://leancloudblog.com/lncld-net-client-hold/)

  估计就是这个原因，导致无法加载

于是捣鼓一番，找了找以前的教程，最终采用了[Livere](https://livere.com/)作为新的评论系统：

1. 打开[官网](https://livere.com/)（应该还是需要梯子的）
   ![](https://baokker-oss-blog-hangzhou.oss-cn-hangzhou.aliyuncs.com/cdn_for_blog/blog_imgs/20220313162429.png)
2. 注册一个Livere账号（信息都是韩文的，得配合Google translation）
3. 回到官方，点击右上角的头像登录，并打开`管理界面`
4. 选择`代码管理`，复制该段代码
   ![](https://baokker-oss-blog-hangzhou.oss-cn-hangzhou.aliyuncs.com/cdn_for_blog/blog_imgs/20220313162350.png)
5. 打开你的blog目录，打开`.\themes\Sakura\layout\_partial\comment.ejs`
6. 将原先Valine插件的代码注释，然后将刚才复制的代码粘贴（如果可以的话，其实可以加上一个逻辑，即当`post.comment == true`时显示评论，我尝试过，但是因为还不是很熟悉语法，所以被迫..其实也没什么大关系，就是在一些例如目录页这样你不希望有评论的地方也可以评论）
7. `hexo g`and`hexo d`，大功告成！



事实证明，来必力除了加载有些慢，and一定绑定一个账号之外，问题不是很大~



