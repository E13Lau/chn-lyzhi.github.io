---
layout: post
title:  "iOS 开发-AVSpeechSynthesizer与AVSpeechUtterance使用简单记录"
date:   2014-12-23 08:59
categories: jekyll update
tags: iOS
---

首先
`#import <AVFoundation/AVFoundation.h>`

于viewDidLoad中初始化

```
- (void)viewDidLoad {
    [super viewDidLoad];
    av = [[AVSpeechSynthesizer alloc]init];
    aaa = [[AVSpeechUtterance alloc]init];
    
    // Do any additional setup after loading the view.
    
}
```

实现方法

```
- (IBAction)Abtn:(id)sender {
    NSString * astring = self.AField.text;
    aaa = [AVSpeechUtterance speechUtteranceWithString:astring];
    aaa.voice = [AVSpeechSynthesisVoice voiceWithLanguage:@"zh-CH"];  //语言
    aaa.rate = 0.2;     //语速
    [av speakUtterance:aaa];
}

-(IBAction)backgroundTap:(id)sender {
    [self.AField resignFirstResponder];
}

- (IBAction)yueyu:(id)sender {
    [self seapkstring:@"zh-HK"];
}

- (IBAction)guoyu:(id)sender {
    [self seapkstring:@"zh-CH"];
}

-(void)seapkstring:(NSString *)language {
    NSString * astring = self.AField.text;
    aaa = [AVSpeechUtterance speechUtteranceWithString:astring];
    aaa.voice = [AVSpeechSynthesisVoice voiceWithLanguage:language];  //语言
    aaa.rate = 0.2;     //语速
    [av speakUtterance:aaa];
}
```