---
layout: post
title:  "iOS 开发-SegueMethon使用记录"
date:   2014-12-06 10:12
categories: jekyll update
tags: iOS
---


```
#pragma mark SegueMethod
-(void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender {
    
    XYZVerifyViewController * verify = segue.destinationViewController;
    if ([[segue identifier] isEqualToString:@"setData"]) {
        verify.content = [NSString stringWithString:self.numberstextField.text];
    }
}

//将要跳转时判断
- (BOOL)shouldPerformSegueWithIdentifier:(NSString *)identifier sender:(id)sender {
    if ([identifier isEqualToString:@"setData"]) {
        if (!self.numberstextField.text.length == 11) {
            return NO;
        }
    }
    return YES;
}
```