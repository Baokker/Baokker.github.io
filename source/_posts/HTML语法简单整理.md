---
title: HTML语法简单整理
author: Baokker
avatar: 'https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/img/custom/avatar.jpg'
authorLink: Baokker.github.io
categories: 技术
comments: true
date: 2021-07-24 19:15:04
tags:
 - HTML
 - 技术
keywords: HTML
description: 菜鸡
photos: https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/blog_imgs/desert-5720527_1920.jpg
---



# HTML

## 速查表

[速查表](https://www.runoob.com/html/html-quicklist.html)



## URL

> **scheme`://`host.domain`:`port`/`path`/`filename**

| 名称     | 功能             | 最常见                                  |
| -------- | ---------------- | --------------------------------------- |
| scheme   | 因特网服务的类型 | http https(安全超文本传输协议) ftp file |
| host     | 域主机           | 默认www                                 |
| domain   | 因特网域名       | 例如baidu.com                           |
| :port    | 主机上的端口号   | 默认80                                  |
| path     | 服务器上的路径   | 如果省略 则文档必须位于网站根目录中     |
| filename | 文档/资源的名称  |                                         |

**只能使用ASCII字符集！！**



## 自己的代码总结

边看边写 把接触到的知识点都罗列了一遍

```html
<!DOCTYPE html>

<html>
    <head style="background-color:pink;">
        <meta charset="utf-8">
        <title>my html notes</title>
        <! style很多时候会用到外部的css文件>
    </head>

    <body>
        <! 注释>

        <h1 style="font-family: 'Courier New', Courier, monospace;color: plum;size: 50px;">my title</h1>
        <h2 style="text-align: center;">my subtitle</h2>

        <! 链接>
        <a href="https://baokker.github.io"><strong><i>blog </strong></i></a>
        <br><br>

        <! 文字样式>
        <p1>my paragraph
        <br><br>

        <! div之后的参数其实可以有很多 例如>
        <! div id="menu" style="background-color:#FFD700;height:200px;width:100px;float:left;">
        <div style="color:rgb(80, 31, 129)">
            <strong>加粗</strong>
            <br><br>

            <em>斜体<span style="color: seagreen;">（而此处颜色发生了改变）</span></em>
            <br><br>
        </div>


        <b>加粗</b>
        <br><br> 

        <i>斜体</i>
        <br><br>

        <sub>下标</sub>
        <br><br>

        <sup>上标</sup>
        <br><br>

        <ins>插入字</ins>
        <br><br>

        <del>删除字</del>
        <br><br>

        <p><abbr title="baokker">bke</abbr> is my abbreviation（缩写）</p>
        <br><br>

        <img border="10" src="https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/img/custom/avatar.jpg" alt="if the image fails to load ,the text will emerge instead">
        <br><br>

        <img border="10" src="https://cdn.jsdelivr.net/gh/Baokker/cdn_for_blog/img/custom/avatar.jpg" alt="if the image fails to load ,the text will emerge instead" style="float:center">居中处理
        <br><br>
        </p1>

        <table border="1" style="background-color: salmon;">
            <caption>table_title</caption>
        <tr>
            <th>name</th>
            <th colspan="2">link</th>
            <! linespan is also useful>
        </tr>
        <tr>
            <td>baokker</td>
            <td><a href="https://baokker.github.io">my blog</a></td>
            <td><a href="https://baidu.com">baidu</a></td>
        </tr></table>
        <br><br>

        <ul>
            <li>coffee</li>
            <li>milk</li>
        </ul>

        <br>

        <ul style="list-style-type: square;">
            <li>coca_cola</li>
            <li>wangzai milk</li>
        </ul>

        <ol>
           <li>wake up</li>
           <li>go to school</li> 
        </ol>

        <br>

        <ol type="i">
            <! type="1" or "A" or "a" is also feasible>
            <li>physics</li>
            <li>chemistry</li>
        </ol>

        <br>
`   
        <form>
            account:<input type="text" name="account"><br>
            password:<input type="password" name="password"><br><br>

            <input type="radio" name="sex" value="male">male<br>
            <input type="radio" name="sex" value="female">female<br><br>

            <input type="checkbox" name="food" value="meat">meat<br>
            <input type="checkbox" name="food" value="vegetabledog">vegetabledog<br><br>

            <select name="food">
                <option value="chinese food" selected>chinese food</option>
                <option value="thai food">thai food</option>
                <option value="french food">french food</option>
            </select><br><br>

        </form>

        <form name="input" action="html_form_action.php" method="get">
            Username: <input type="text" name="user">
            <input type="submit" value="Submit"><br>
            注意 action文件并不存在 本例仅作为示例<br><br>
        </form>

        <iframe src="https://baokker.github.io" name="example" height="600" width="600"></iframe>
        <br><br>
        <a href="https://www.runoob.com/html/html-colornames.html" target="example">点击此链接可以看菜鸟教程</a>
        <br><br>

        <div style="background-color: rgba(25,65,25,0.7);">
        <br><br>
        </div>

        <br><br>

        <p id="mydemo">测试语句 用于示例script</p><br>

        <button type="button" onclick="example()">点击此处会修改测试语句</button>

        <script>
            function example()
            {
                document.getElementById("mydemo").innerHTML="hahahahaha";
            };
        </script>
        <noscript>sorry script无法测试 浏览器不支持JavaScript！</noscript>

        <br><br>

        <p>字符实体<br>
        &lt;&#60;&gt;&#62;等等 参照<a href="https://www.runoob.com/html/html-entities.html">这个链接</a><br><br>    </p>
        
        <! 计算机输出>
        <code>直接输出</code>
        <samp>sample</samp>
        <var></var>

    </body>
</html>

```



---

该图片由<a href="https://pixabay.com/zh/users/jbi-weisendorf-5797981/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=5720527">Jürgen Bierlein</a>在<a href="https://pixabay.com/zh/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=5720527">Pixabay</a>上发布