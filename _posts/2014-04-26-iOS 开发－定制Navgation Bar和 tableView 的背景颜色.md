---
layout: post
title:  "iOS 开发－定制Navgation Bar和 tableView 的背景颜色"
date:   2014-04-26 00:50
categories: jekyll update
tags: iOS
---

Navgation Bar部分：

```
@implementation XYZAppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    [[UINavigationBar appearance] setBarTintColor:[UIColor colorWithRed:47.0/255.0 green:197.0/255.0 blue:254.0/255.0 alpha:1.0f]];
    return YES;
}
```

其中[UIColor ＊]还可以是
`[[UINavigationBar appearance] setBarTintColor:[UIColor redcolor];`

tableView部分：

```
@implementation XYZToDoListTableViewController
- (void)viewDidLoad
{
    [super viewDidLoad];
    [self setBGcolor];
}
-(void)setBGcolor
{
    CGFloat R  = (CGFloat) 252/255.0;
    CGFloat G = (CGFloat) 252/255.0;
    CGFloat B = (CGFloat) 252/255.0;
    CGFloat alpha = (CGFloat) 1.0;
    UIColor *myColorRGB = [ UIColor colorWithRed: R  green: G  blue: B  alpha: alpha  ];
    self.tableView.backgroundColor = myColorRGB;
}
```

UIColor官方API文档
[UIColor Class Reference](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIColor_Class/Reference/Reference.html#jumpTo_3)