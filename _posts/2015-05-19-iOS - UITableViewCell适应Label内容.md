---
layout: post
title:  "iOS - UITableViewCell适应Label内容"
date:   2015-05-19 14:09
categories: jekyll update
tags: iOS
---

环境：</br>
iOS SDK 8.3</br>
Xcode 6.3.1

参考链接： 
[Auto Layout 使用心得（五）—— 根据文字、图片自动计算UITableViewCell 高度](http://lvwenhan.com/ios/449.html)

以及代码： 
<https://github.com/johnlui/AutoLayout>

添加Cell的约束，其中lable的行数改为0，其中xib中的contentView的高度并不需要固定，完全可以自由发挥。

ViewController中，需要注册一个这个cell，以便复用，以及添加下列两行代码

```
self.texttableView.estimatedRowHeight = 80.f;
self.texttableView.rowHeight = UITableViewAutomaticDimension;
```

至此应该能实现cell动态高度。该方法仅支持 iOS 8 +