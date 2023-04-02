---
title: "Hugo折腾记录" #标题
date: 2023-03-04T23:44:32+08:00 #创建时间
lastmod: 2023-03-05T23:44:32+08:00 #更新时间
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
    image: "img/Pictures/" #图片路径：
    caption: "" #图片底部描述
    alt: ""
    relative: false
---





在终端直接输入hugo server -D就可以在本地预览了，本地预览网址为 localhost:1313， 输入hugo就可以生成public文件夹，这个文件夹可以部署到云服务器或者托管到github上， 注意：输入hugo的生成方式只会往public文件夹里添加内容，但是不会删除外部已经不存在而public里面还存在的文件， 所以我一般用hugo -F --cleanDestinationDir命令，表示每次生成的public都是全新的，会覆盖原来的。 

