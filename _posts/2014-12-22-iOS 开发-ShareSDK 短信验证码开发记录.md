---
layout: post
title:  "iOS 开发-ShareSDK 短信验证码开发记录"
date:   2014-12-22 14:53
categories: jekyll update
tags: iOS
---

申请SDK Key 并导入SMS_SDK。

在 appDelegate 添加
`#import <SMS_SDK/SMS_SDK.h>`

在 - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 方法中添加
`[SMS_SDK registerApp:appKey withSecret:appSecret];`

响应方法中添加获取验证码

```
if (!(self.numberstextField.text.length == 11)) { //简单检测是否为11个数字手机号码
        NSString *title = [NSString stringWithFormat:@"警告⚠"];
        NSString  *message = [NSString stringWithFormat:@"请完整输入手机号码"];
        [[[UIAlertView alloc]initWithTitle:title message:message delegate:self cancelButtonTitle:@"确定" otherButtonTitles:nil, nil]show];
    }else { //检测网络功能
        NetworkStatus networkStatus = [Reachability reachabilityForInternetConnection].currentReachabilityStatus;
        if (networkStatus == NotReachable) {
            NSLog(@"AAAA");
            NSString *title = [NSString stringWithFormat:@"警告⚠"];
            NSString  *message = [NSString stringWithFormat:@"请检测网络连接"];
            [[[UIAlertView alloc]initWithTitle:title message:message delegate:self cancelButtonTitle:@"确定" otherButtonTitles:nil, nil]show];
        }else { //请求验证码
        [SMS_SDK getVerifyCodeByPhoneNumber:self.numberstextField.text AndZone:@"86" result:^(enum SMS_GetVerifyCodeResponseState state) { //回调，0为失败，1为成功
            switch (state) {
                case 0:{
                    NSLog(@"获取失败");
                    [self.numberstextField becomeFirstResponder];
                    self.warnLabel.text = @"获取失败";
                    self.warnLabel.hidden = NO;
                    [NSTimer scheduledTimerWithTimeInterval:0.8 target:self selector:@selector(removeWarnLabel:) userInfo:nil repeats:NO];
                    break;
                }
                case 1:{
                    NSLog(@"获取成功");
                    [self.yanzhengmatextField becomeFirstResponder];
                    self.warnLabel.text = @"获取成功";
                    self.warnLabel.hidden = NO;
                    [NSTimer scheduledTimerWithTimeInterval:0.8 target:self selector:@selector(removeWarnLabel:) userInfo:nil repeats:NO];
                    secondsCountDown = 30;
                    countDownTimer = [NSTimer scheduledTimerWithTimeInterval:1 target:self selector:@selector(timeFireMethod) userInfo:nil repeats:YES];//1秒运行一次，若secondsCountDown==0则停止。
                    self.getVerifyBtn.enabled = false;
                    break;
                }
                default:
                    break;
            }
        }];
        }
    }
```

响应方法中添加检查验证码

```
[self.numberstextField resignFirstResponder];
    [self.yanzhengmatextField resignFirstResponder];
    
    //待添加检测网络功能
    [SMS_SDK commitVerifyCode:self.yanzhengmatextField.text result:^(enum SMS_ResponseState state) {
        switch (state) {
            case 0: {
                NSLog(@"验证失败");
                self.warnLabel.text = @"验证失败";
                self.warnLabel.hidden = NO;
                [NSTimer scheduledTimerWithTimeInterval:0.8 target:self selector:@selector(removeWarnLabel:) userInfo:nil repeats:NO];
                break;
            }
            case 1: {
                NSLog(@"验证成功");
                NSString *title = [NSString stringWithFormat:@"成功"];
                NSString  *message = [NSString stringWithFormat:@"验证成功"];
                [[[UIAlertView alloc]initWithTitle:title message:message delegate:self cancelButtonTitle:@"确定" otherButtonTitles:nil, nil]show];
                break;
            }
            default:
                break;
        }
    }];
```

碎块

```
//button设置为30秒倒计时
-(void)timeFireMethod {
    secondsCountDown--;
    [self.getVerifyBtn setTitle:[NSString stringWithFormat:@"下次获取%d秒",secondsCountDown] forState:UIControlStateNormal];
    if(secondsCountDown==0){
        [countDownTimer invalidate];
        [self.getVerifyBtn setTitle:[NSString stringWithFormat:@"获取验证码"] forState:UIControlStateNormal];
        self.getVerifyBtn.enabled = true;
    }
}
```