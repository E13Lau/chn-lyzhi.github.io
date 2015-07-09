---
layout: post
title:  "iOS 开发-UIAutomation 记录"
date:   2015-06-08 13:59
categories: jekyll update
tags: iOS
---

```
var target = UIATarget.localTarget();
var app = target.frontMostApp();
var window = app.mainWindow();
var tabBar = app.tabBar();
var tabButton = tabBar.buttons()["More"];
target.logElementTree();
tabButton.tap()
//target.tap({x:137, y:416})
window.buttons()[0].tap()
```

資料：
<https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/UsingtheAutomationInstrument/UsingtheAutomationInstrument.html#//apple_ref/doc/uid/TP40004652-CH20-SW1>

<http://adcdownload.apple.com//wwdc_2010/wwdc_2010_video_assets__pdfs/306__automating_user_interface_testing_with_instruments.pdf>

<http://www.cnblogs.com/vowei/archive/2012/08/10/2631949.html>

<http://kingson.org/?p=345>

<http://www.infoq.com/cn/articles/build-ios-continuous-integration-platform-part1>

<http://www.infoq.com/cn/news/2015/04/ios-testing-ci>

<http://bbs.sjtu.edu.cn/bbstcon?board=MobileDev&reid=1354974523>
