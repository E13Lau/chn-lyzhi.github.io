---
layout: post
title:  "PC+谷歌浏览器部署GoAgent番羽墙"
date:   2014-04-17 22:36
categories: jekyll update
tags: windows
---

* 上去谷歌创建一个GAE应用
* 在GoAgent添上ID，上传
* 配置谷歌浏览器插件

[GAE应用地址](https://appengine.google.com/)

[GoAgent地址](https://code.google.com/p/goagent/)

[谷歌switchysharp插件地址](https://code.google.com/p/switchysharp/)

第一步创建GAE应用

第二步部署本地GoAgent

修改localproxy.ini中的[gae]下的appid=你的appid(多appid请用|隔开)

双击serveruploader.bat(Mac/Linux上传方法请见FAQ)，上传成功后即可使用了(地址127.0.0.1:8087)

第三部配置谷歌浏览器

安装插件，导入设置