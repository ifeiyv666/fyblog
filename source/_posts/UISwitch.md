---
title: UISwitch(Objc)
categories:
  - Objective-C
abbrlink: 10139
tags:
  - UISwitch
date: 2017-04-06 18:42:27
---

#### UISwitch

```objc

#import "ViewController.h"

@interface ViewController ()

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
//    初始化并设置frame
    UIStepper *stepper = [[UIStepper alloc]initWithFrame:CGRectMake(100, 100, 100, 100)];
//    最小值
    stepper.minimumValue = 0;
    
//    最大值
    stepper.maximumValue = 10;
//    设置当前值
    stepper.value = 4;
//    设置每次+2或-2，默认是1
    stepper.stepValue = 2;
    
//    设置颜色
    [stepper setTintColor:[UIColor orangeColor]];
//    添加事件
    [stepper addTarget:self action:@selector(valueChange:) forControlEvents:UIControlEventValueChanged];
    
//    处理事件是否一直回调，默认是YES
    stepper.continuous = YES;
    
//    设置能否重复操作，默认是YES
    stepper.autorepeat = YES;
    
//    设置是否能循环，默认是NO
    stepper.wraps = YES;
    
    [self.view addSubview:stepper];
}
-(void)valueChange:(UIStepper*)stepper{
    NSLog(@"%lf",stepper.value);
}
@end


```


