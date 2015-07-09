---
layout: post
title:  "OS X - 安装Scrapy与lxml的过程中的问题。"
date:   2015-03-16 11:58
categories: jekyll update
tags: OS X
---

当尝试使用`sudo pip install lxml`来安装 lxml 时

提示

***Command "/usr/bin/python -c "import setuptools, tokenize;__file__='/private/tmp/pip-build-Swce2X/lxml/setup.py';exec(compile(getattr(tokenize, 'open', open)(__file__).read().replace('\r\n', '\n'), __file__, 'exec'))" install --record /tmp/pip-bXUbas-record/install-record.txt --single-version-externally-managed --compile" failed with error code 1 in /private/tmp/pip-build-Swce2X/lxml***

使用以下网页的方法

[MAC OSX下include头文件缺失引起的问题及解决办法, command line tools 安装](http://blog.marchtea.com/archives/104)

安装 `command line tools` 即可成功安装`lxml`与`Scrapy`