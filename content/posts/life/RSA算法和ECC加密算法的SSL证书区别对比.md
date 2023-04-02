---
title: "RSA算法和ECC加密算法的SSL证书区别对比" #标题
date: 2023-03-11T21:39:01+08:00 #创建时间
lastmod: 2023-03-12T21:39:01+08:00 #更新时间
author: ["木木"] #作者
categories: 
- 日常
- 随笔
tags: 
- Daily
- Life
description: "" #描述
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: false #是否展示评论
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true #顶部显示当前路径
cover:
    image: "img/Pictures/2.png" #图片路径：
    caption: "" #图片底部描述
    alt: ""
    relative: false
---

**RSA 算法和 ECC 加密算法的SSL证书区别对比**

RSA算法和ECC算法是目前流行的主要的两种 SSL证书公钥加密算法。

当然还有刚刚兴起的国密SM2加密算法，但由于国密算法的 SSL证书目前仅仅两三款浏览器支持，且需要相应的服务器环境支持，所以本文不做过多介绍。

**RSA算法：**比较常见的算法，应用较早，为普及，比 ECC算法的适用范围更广，兼容性很好，一般采用 2048 位的加密长度，但是对服务端性能消耗高。

**ECC算法：**中文名称为椭圆加密算法，新一代算法趋势主流，一般采用 256 位加密长度，加密速度快，效率更高，对服务器资源消耗低，而且重要的是更安全，抗攻击型更强。

![image-20230313002253077](https://img.l50.top/file/3c9ce959d54679cff0b18.png)
