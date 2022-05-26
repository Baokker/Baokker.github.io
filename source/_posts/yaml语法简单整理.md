---
title: yaml语法简单整理
author: Baokker
avatar: 'https://raw.githubusercontent.com/Baokker/cdn_for_blog/main/img/custom/avatar.jpg'
authorLink: https://Baokker.github.io
categories: 随想
comments: true
date: 2021-07-21 15:40:04
tags:
- 技术
keywords: yaml
description: yaml简单整理
photos: https://raw.githubusercontent.com/Baokker/cdn_for_blog/main/blog_imgs/yaml1.png
---

# Yaml

> yaml ain't markup language

配置Sakura主题的时候用到了yaml 当时看着语法还挺清晰 依样画葫芦也能写出来 就直接上手了 写blog的时候倒是经常因为冒号后面没加空格之类的error而报错 现在来总结下：

[参考链接](https://www.runoob.com/w3cnote/yaml-intro.html)

## 基本语法规则：

> - 大小写敏感
>
> - 使用缩进表示层级关系
> - 缩进不允许使用tab，只允许空格
> - 缩进的空格数不重要，只要相同层级的元素左对齐即可
> - '#'表示注释

这方面个人感觉 除了不允许tab外 和py的类似之处很多



## 数据类型

> - 对象：键值对的集合，又称为映射（mapping）/ 哈希（hashes） / 字典（dictionary）
> - 数组：一组按次序排列的值，又称为序列（sequence） / 列表（list）
> - 纯量（scalars）：单个的、不可再分的值

类似于py的dict/list/常量



### 对象

```yaml
key:{key1: value1, key2: value2, ...} # 冒号后面要加一个空格！


key: 
    child-key: value
    child-key2: value2
    
?  # 较为复杂时
    - complexkey1
    - complexkey2
:
    - complexvalue1
    - complexvalue2

```



### 数组

```yaml
- A
- B
- C

- # 子成员是一个数组
 - A
 - B
 - C

key: [v1,v2,..]
```



综合展示：

- ```yaml
  companies:
      -
          id: 1
          name: company1
          price: 200W
      -
          id: 2
          name: company2
          price: 500W
  
  ```

- ```yaml
  # flow
  companies: [{id: 1,name: company1,price: 200W},{id: 2,name: company2,price: 500W}]
  # 很像Python的字典表达方式哈
  ```

  

显然 二者可以混合使用



## 常量

上代码

```yaml
boolean: 
    - TRUE  #true,True都可以
    - FALSE  #false，False都可以
float:
    - 3.14
    - 6.8523015e+5  #可以使用科学计数法
int:
    - 123
    - 0b1010_0111_0100_1010_1110    #二进制表示
null:
    nodeName: 'node'
    parent: ~  #使用~表示null
string:
    - 哈哈
    - 'Hello world'  #可以使用双引号或者单引号包裹特殊字符
    - newline
      newline2    #字符串可以拆成多行，每一行会被转化成一个空格
date:
    - 2018-02-17    #日期必须使用ISO 8601格式，即yyyy-MM-dd
datetime: 
    -  2018-02-17T15:02:31+08:00    #时间使用ISO 8601格式，时间和日期之间使用T连接，最后使用+代表时区
```



## 变量引用

```yaml
default-db:
  port: 3306

user-db:
  port: ${default-db.port}
```

可以用形如上述的方法进行变量引用（但是 反过来赋值是不行的！）

此外 可用**&和***进行引用和赋值：

```yaml
defaults: &defaults # 名称自定义
  adapter:  postgres
  host:     localhost

development:
  database: myapp_development
  <<: *defaults

test:
  database: myapp_test 
  <<: *defaults # << 表示合并到当前 *类似于解引用hhh
  
- &showell Steve 
- Clark 
- Brian 
- Oren 
- *showell 
```

相当于

```yaml
defaults:
  adapter:  postgres
  host:     localhost

development:
  database: myapp_development
  adapter:  postgres
  host:     localhost

test:
  database: myapp_test
  adapter:  postgres
  host:     localhost
  
- &showell Steve 
- Clark 
- Brian 
- Oren 
- Steve
```

# 强制类型转换

用!!

```yaml
e: !!str 123
f: !!str true
```

