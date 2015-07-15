---
layout: post
title:  "2015-07-15-iOS 开发-AutoLayout 朋友圈"
date:   2015-07-15 08:39
categories: jekyll update
tags: iOS
---


Tips：
Storyboard 创建的 TableView、Cell不需要 New、注册

```
self.myTableView.estimatedRowHeight = 395.f;
self.myTableView.rowHeight = UITableViewAutomaticDimension;
```
这两句让 TableView 实现动态高度

</br>

ImageView 高宽约束应设置为 小于等于，这样才会在为 nil 时自动隐藏且不会占位

当 ScrollView 包括 Table、Collation 的 Top 或者 Bottom 约束是相对于 Guide 的 Top 时，内容经过 Nav、TabBar 不会出现透明效果

View Controller 的 Adjust Scroll View Insets 打勾，TableView 里面的 Content 自动往下退 64 点，