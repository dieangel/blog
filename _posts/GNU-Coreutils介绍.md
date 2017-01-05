---
title: GNU Coreutils介绍
toc: true
date: 2016-12-28 11:54:29
tags: [GNU, Linux]
categories: 
- Linux
- GNU Coreutils
---
**GNU核心工具组（英语：GNU Core Utilities，亦常缩写为Coreutils）**是一个包含了多个类Unix所需的基本工具的软件包，其亦是之前许多类似软件包（如textutils（文本工具组）、shellutils（shell工具组）、fileutils（文件工具组）等）所包含工具的集合[注1][1]。
[1]: https://zh.wikipedia.org/wiki/GNU%E6%A0%B8%E5%BF%83%E5%B7%A5%E5%85%B7%E7%BB%84
<!--more-->
# 常规选项
这套工具集里面的程序大多支持一些共有的选项。一般来说，程序的**选项**或者**操作数**的顺序不重要，`sort -r passwd -t :`对程序来说和`sort -r -t : passwd`是一样的（这里`:`是选项`-t`的参数）。
但是，当**POSIXY_CORRECT**这个环境变量已经设置了的话，**选项**就**必须在**操作数之前。
某些程序可能有一个在尾部的`-`参数。在这样的程序里，即使**POSIXY_CORRECT**没有设置，也要将选项放在操作数前。如**env**命令。
某些程序在只有一个命令行参数的时候会识别`--version --help`选项。`--`选项会不再其后带`-`的参数识别为操作数。`sort -- -r`会从 `-r` 文件读取输入。
## 退出状态
基本上每个程序都会产生一个整型的退出状态。普遍情况下`0`表示成功，`非0`表示失败。
## 备份选项
一些GNU程序（如`cp, install, ln, mv`）可选地在写新的版本前进行备份。这些选项控制了备份的细节。
- -b/--backup=[*method*] 
