---
layout: post
title:  "iOS - 用Hopper反编译 Nike+ 二进制文件"
date:   2015-05-09 10:48
categories: jekyll update
tags: iOS
---

用`Hopper`反编译iOS App二进制文件，IPA里的二进制文件经过`Hopper`反编译后，能可视化文件的结构，存储的敏感信息如果以字符串常量写在程序中则会暴露无疑。

从 iTunes 的App Store 中下载 Nike+ Running 的 ipa 文件

* 解压 ipa 文件
* 打开Payload文件夹
* 右键”NikePlus”显示包内容
* 找到 NikePlus 文件，并在Hopper打开