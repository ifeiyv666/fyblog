---
title: UIsegementControl(Objc)
categories:
  - Objective-C
abbrlink: 10136
tags:
  - UIsegementControl
date: 2017-03-21 13:34:29
---

#### UIsegementControl

```objc
#import "ViewController.h"

@interface ViewController ()

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
//    初始化UISegmentedControl
    UISegmentedControl *segmentControl = [[UISegmentedControl alloc]initWithFrame:CGRectMake(100, 100, 200, 50)];
//    设置背景色
    segmentControl.backgroundColor = [UIColor yellowColor];
//    添加第一段
    [segmentControl insertSegmentWithTitle:@"第一段" atIndex:0 animated:YES];
//    添加第二段
    [segmentControl insertSegmentWithTitle:@"第二段" atIndex:1 animated:YES];
//    添加第三段
//    设置文字和图片，谁在后面，显示谁
    [segmentControl insertSegmentWithTitle:@"第三段" atIndex:2 animated:YES];
    
    UIImage *image = [UIImage imageNamed:@"qq"];
//    显示原始图片
    image = [image imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
//    [segmentControl insertSegmentWithImage: image atIndex:2 animated:YES];
    [segmentControl setImage:image forSegmentAtIndex:2];
    
 
//    选中颜色
    segmentControl.tintColor = [UIColor redColor];
//    设置选中某一段
    segmentControl.selectedSegmentIndex = 1;
    
//    获取某一段的title
    NSString *title = [segmentControl titleForSegmentAtIndex:1];
    NSLog(@"title = %@",title);
//    添加响应事件
    [segmentControl addTarget:self action:@selector(valueChange:) forControlEvents:UIControlEventValueChanged];
    
    [self.view addSubview:segmentControl];
    
}
-(void)valueChange:(UISegmentedControl*)seg{

    NSInteger index = seg.selectedSegmentIndex;
    switch (index) {
        case 0:{
            NSLog(@"0");
            
            UIAlertView *alert = [[UIAlertView alloc]initWithTitle:@"提示" message:@"还钱" delegate:self cancelButtonTitle:@"确定" otherButtonTitles:@"不还", nil];
            [alert show];
        }
            break;
        case 1:
            NSLog(@"1");
            break;
        case 2:
            NSLog(@"2");
            break;
            
        default:
            break;
    }
}

@end

```
