---
layout: post
title:  "iOS 开发-UIPickerView使用记录"
date:   2015-01-10 10:16
categories: jekyll update
tags: iOS
---


简单记录一下

```
//
//  CalorieViewController.m
//  ISport
//
//  Created by command.Zi on 15/1/9.
//  Copyright (c) 2015年 yundu. All rights reserved.
//

#import "CalorieViewController.h"

@interface CalorieViewController () {
    NSMutableArray * projectName;
    NSMutableArray * power;
    NSMutableArray * time;
    NSMutableArray * bigArray;
}

- (IBAction)disMissButton:(id)sender;

@property (strong, nonatomic) IBOutlet UIPickerView *pickerView;

@end

@implementation CalorieViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    projectName = [[NSMutableArray alloc]init];
    power = [[NSMutableArray alloc]init];
    time = [[NSMutableArray alloc]init];
    [time addObject:@"0.5小时"];
    for (int i = 1; i<9; i++) {
        NSString * string = [NSString stringWithFormat:@"%d小时",i];
        [time addObject:string];
    }

    NSString *filePath=[[NSBundle mainBundle] pathForResource:@"Ca" ofType:@"plist"];
    bigArray = [[NSMutableArray alloc]initWithContentsOfFile:filePath];
//    NSLog(@"%@",bigArray);
    
    self.pickerView.delegate = self;
    self.pickerView.dataSource = self;
    // Do any additional setup after loading the view from its nib.
}

- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

-(NSInteger)numberOfComponentsInPickerView:(UIPickerView *)pickerView {
    return 3;
}

-(NSInteger)pickerView:(UIPickerView *)pickerView numberOfRowsInComponent:(NSInteger)component {
    if (component == 1) {
        return [bigArray[[self.pickerView selectedRowInComponent:0]][1] count];
    }else {
        return [bigArray count];
    }
}

-(NSString *)pickerView:(UIPickerView *)pickerView titleForRow:(NSInteger)row forComponent:(NSInteger)component {
    NSString * string = @"无数据";
    if (component == 0) {
        return bigArray[row][0];
    }
    if (component == 1) {
        return bigArray[[self.pickerView selectedRowInComponent:0]][1][row];
    }
    if (component == 2) {
        return time[row];
    }else {
        return string;
    }
}

-(void)pickerView:(UIPickerView *)pickerView didSelectRow:(NSInteger)row inComponent:(NSInteger)component {
    if (component == 0) {
        [self.pickerView reloadComponent:1]; //更新第二组pickerView
    }
}

/*
#pragma mark - Navigation

// In a storyboard-based application, you will often want to do a little preparation before navigation
- (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender {
    // Get the new view controller using [segue destinationViewController].
    // Pass the selected object to the new view controller.
}
*/

- (IBAction)disMissButton:(id)sender {
    [self.navigationController popViewControllerAnimated:YES];
}

@end
```

其中bigArray的结构为
`[[object,[object,object]][object,[object]]]`