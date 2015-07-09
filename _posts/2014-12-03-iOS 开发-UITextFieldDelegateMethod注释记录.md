---
layout: post
title:  "iOS 开发-UITextFieldDelegateMethod注释记录"
date:   2014-12-03 17:09
categories: jekyll update
tags: iOS
---


```
#pragma mark UITextFieldDelegateMethod
//当输入框被激活
- (BOOL)textFieldShouldBeginEditing:(UITextField *)textField {
    return YES;
}
//当输入框被激活
- (void)textFieldDidBeginEditing:(UITextField *)textField {
    
}
//当输入框取消激活
- (BOOL)textFieldShouldEndEditing:(UITextField *)textField {
    return YES;
}
//当输入框取消激活
- (void)textFieldDidEndEditing:(UITextField *)textField {
    
}
//当输入框值（string）开始改变时...
- (BOOL)textField:(UITextField *)textField shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string {
    NSLog(@"%@",string);
    return YES;
}

- (BOOL)textFieldShouldClear:(UITextField *)textField {
    return YES;
}
- (BOOL)textFieldShouldReturn:(UITextField *)textField {
    return YES;
}
```