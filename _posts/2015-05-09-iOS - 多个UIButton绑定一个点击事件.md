---
layout: post
title:  "iOS - 多个UIButton绑定一个点击事件"
date:   2015-05-09 10:44
categories: jekyll update
tags: iOS
---

多个UIButton绑定一个点击事件，每个Button的运行方法不同的实现之一。

Xib中有多个Button，每个Button绑定一个IBOutlet
这样

```
@property (strong, nonatomic) IBOutlet UIButton *activityStartButton;  
@property (strong, nonatomic) IBOutlet UIButton *activityEndButton;
```

在Xib中给每个Button添加一个Restoration ID

给每个Button添加点击事件

```
- (void)initActionButton {  
    [self.activityStartButton addTarget:self action:@selector(touchDownWithButton:) forControlEvents:UIControlEventTouchDown];  
    [self.activityEndButton addTarget:self action:@selector(touchDownWithButton:) forControlEvents:UIControlEventTouchDown];  
}
```

实现点击事件

```
#pragma mark - ViewAction
- (void)touchDownWithButton:(UIButton *)button {
    if ([button.restorationIdentifier isEqualToString:@"activityStartButton"]) {
        
    }
    if ([button.restorationIdentifier isEqualToString:@"activityEndButton"]) {
        
    }
}
```