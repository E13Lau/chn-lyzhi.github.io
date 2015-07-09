---
layout: post
title:  "iOS－创建依赖组件的pickerView"
date:   2015-01-19 17:13
categories: jekyll update
tags: iOS
---

```
-(NSInteger)numberOfComponentsInPickerView:(UIPickerView *)pickerView {
    return 3;
}

-(NSInteger)pickerView:(UIPickerView *)pickerView numberOfRowsInComponent:(NSInteger)component {
    if (component == 0) {
        
        return bigArray.count;
    }
    if (component == 1) {
        componentIndex = [self.pickerView selectedRowInComponent:0];
        
        return [bigArray[componentIndex][1] count];
    }
    if (component == 2) {
        return time.count;
    }
    return  0;
}

-(NSString *)pickerView:(UIPickerView *)pickerView titleForRow:(NSInteger)row forComponent:(NSInteger)component {
    NSString * string = @"无数据";
    
    if (component == 0) {
        return bigArray[row][0];
    }
    if (component == 1) {
        NSString * powerString = [bigArray[componentIndex][1][row] objectForKey:@"power"];
            return powerString;
    }
    if (component == 2) {
        return time[row];
    }else {
        return string;
    }
}

-(void)pickerView:(UIPickerView *)pickerView didSelectRow:(NSInteger)row inComponent:(NSInteger)component {
    if (component == 0) {
        [self.pickerView reloadComponent:1];
         //更新第二组pickerView
    }
    if (component == 1) {
        b = [[bigArray[componentIndex][1][row] objectForKey:@"K"] floatValue];
    }
    if (component == 2) {
        c = [time[row] floatValue]*60;
    }
    
    [self.textField resignFirstResponder];
}
```

其中`componentIndex`为一个`NSInteger  componentIndex`变量。

用于保存第一组所选择的下标，根据这个下标更新第二组的数量和数组。
如果不用单独的变量保存，则会因为第二组的更新不及时，其数据溢出而报错。

下面为m文件完整代码：

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
    float b;
    float c;
    NSInteger  componentIndex;
    
}

- (IBAction)disMissButton:(id)sender;

@property (strong, nonatomic) IBOutlet UIPickerView *pickerView;
@property (strong, nonatomic) IBOutlet UITextField *textField;
@property (strong, nonatomic) IBOutlet UILabel *calLabel;
- (IBAction)getButton:(id)sender;

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
    
    b = 0.1564;
    c = 0.5*60;
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
    if (component == 0) {
        
        return bigArray.count;
    }
    if (component == 1) {
        componentIndex = [self.pickerView selectedRowInComponent:0];
        
        return [bigArray[componentIndex][1] count];
    }
    if (component == 2) {
        return time.count;
    }
    return  0;
}

-(NSString *)pickerView:(UIPickerView *)pickerView titleForRow:(NSInteger)row forComponent:(NSInteger)component {
    NSString * string = @"无数据";
    
    if (component == 0) {
        return bigArray[row][0];
    }
    if (component == 1) {
        NSString * powerString = [bigArray[componentIndex][1][row] objectForKey:@"power"];
            return powerString;
    }
    if (component == 2) {
        return time[row];
    }else {
        return string;
    }
}

-(void)pickerView:(UIPickerView *)pickerView didSelectRow:(NSInteger)row inComponent:(NSInteger)component {
    if (component == 0) {
        [self.pickerView reloadComponent:1];
         //更新第二组pickerView
    }
    if (component == 1) {
        b = [[bigArray[componentIndex][1][row] objectForKey:@"K"] floatValue];
    }
    if (component == 2) {
        c = [time[row] floatValue]*60;
    }
    
    [self.textField resignFirstResponder];
}

-(NSString *)getCalorie {
    if (!self.textField) {
        return nil;
    }else {
        float A = [self.textField.text floatValue];
        float cal = A*b*c;
        self.calLabel.text = [NSString stringWithFormat:@"%f",cal];
    }
    
    return @"d";
}
/*
#pragma mark - Navigation

// In a storyboard-based application, you will often want to do a little preparation before navigation
- (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender {
    // Get the new view controller using [segue destinationViewController].
    // Pass the selected object to the new view controller.
}
*/

-(IBAction)backgroundTap:(id)sender {
    [self.textField resignFirstResponder];
}

- (IBAction)disMissButton:(id)sender {
    [self.navigationController popViewControllerAnimated:YES];
}

- (IBAction)getButton:(id)sender {
    [self.textField resignFirstResponder];
    [self getCalorie];
}

@end
```