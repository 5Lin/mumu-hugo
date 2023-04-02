---
title: "Git Core.autocrlf配置说明" #标题
date: 2023-03-03T23:18:19+08:00 #创建时间
lastmod: 2023-03-04T23:18:19+08:00 #更新时间
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

### 格式化

格式化是许多开发人员在协作时，特别是在跨平台情况下，遇到的令人头疼的细小问题。 由于编辑器的不同或者Windows程序员在跨平台项目中的文件行尾加入了回车换行符， 一些细微的空格变化会不经意地进入大家合作的工作或提交的补丁中。不用怕，Git的一些配置选项会帮助你解决这些问题。

### core.autocrlf

假如你正在Windows上写程序，又或者你正在和其他人合作，他们在Windows上编程，而你却在其他系统上，在这些情况下，你可能会遇到行尾 结束符问题。 这是因为Windows使用回车和换行两个字符来结束一行，而Mac和Linux只使用换行一个字符。 虽然这是小问题，但它会极大地扰乱跨平台协作。

在Windows平台上，git默认的core.autocrlf是true，可以通过`git config --list`命令查看。

Git可以在你提交时自动地把行结束符CRLF转换成LF，而在签出代码时把LF转换成CRLF。用`core.autocrlf`来打开此项功能， 如果是在Windows系统上，把它设置成`true`（默认配置），这样当签出代码时，LF会被转换成CRLF：

```csharp
Copy$ git config --global core.autocrlf true
```

Linux或Mac系统使用LF作为行结束符，因此你不想Git在签出文件时进行自动的转换；当一个以CRLF为行结束符的文件不小心被引入时你肯定想进行修正， 把`core.autocrlf`设置成input来告诉Git在提交时把CRLF转换成LF，签出时不转换：

```verilog
Copy$ git config --global core.autocrlf input
```

这样会在Windows系统上的签出文件中保留CRLF，会在Mac和Linux系统上，包括仓库中保留LF。

如果你是Windows程序员，且正在开发仅运行在Windows上的项目，可以设置`false`取消此功能，把回车符记录在库中：

```csharp
Copy$ git config --global core.autocrlf false
```

关于在IDEA中的提示，如下图所示，点击`FIX AND COMMIT`即可。
![img](https://img2018.cnblogs.com/blog/1577027/201907/1577027-20190725140322466-21269825.png)
