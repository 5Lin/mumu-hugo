---
title: "Hugo备份以及遇到的问题" #标题
date: 2023-03-01T22:48:26+08:00 #创建时间
lastmod: 2023-03-03T22:48:26+08:00 #更新时间
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
    image: "img/Pictures/1.png" #图片路径：
    caption: "" #图片底部描述
    alt: ""
    relative: false
---

当你在Windows下搭建hugo时你必须首先将git配置中的自动切换改为false，如果不调整该项，你通过Windows上传的hugo到github pages将会样式不对，即使你在本地预览的是正确的主题，你应当在操作之前使用：`git config core.autocrlf false`。

至于为什么，详情见另外一文 《git core.autocrlf配置说明》



