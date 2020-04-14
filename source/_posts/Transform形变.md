---
title: Transform形变(Objc)
categories:
  - Objective-C
abbrlink: 10129
tags:
  - Transform
date: 2017-03-19 16:29:10
---

#### Transform形变

```objc
#import "RootViewController.h"

@interface RootViewController ()

@end

@implementation RootViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
//    [self transform];
    [self lastTransform];
}
#
-(void)lastTransform{
    UIView *changeView = [[UIView alloc]initWithFrame:CGRectMake(100, 100, 100, 100)];
    changeView.tag = 20;
    changeView.backgroundColor = [UIColor yellowColor];
    [self.view addSubview:changeView];
    
    UIButton *button = [UIButton buttonWithType:UIButtonTypeCustom];
    button.frame = CGRectMake(50, 50, 50, 50);
    button.backgroundColor = [UIColor blueColor];
    [button addTarget:self action:@selector(onClick) forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button];
}
-(void)onClick{
    
//     仿射变化
//    通过center bounds transform来控制要显示的内容
    UIView *changeView = [self.view viewWithTag:20];
//    在上次形变的基础上，继续形变
    changeView.transform = CGAffineTransformTranslate(changeView.transform, 10, 0);
    
//    旋转
   CGFloat angle = [self getAgreeFromDegree:10];
    changeView.transform = CGAffineTransformRotate(changeView.transform, angle);

//    缩放
//    changeView.transform = CGAffineTransformScale(changeView.transform, 0.9, 1.0);
    NSLog(@"%@",NSStringFromCGRect(changeView.frame));
    NSLog(@"%f",changeView.bounds.size.width);
    NSLog(@"%f",changeView.bounds.size.height);
    NSLog(@"%f",changeView.center.x);
    NSLog(@"%f",changeView.center.y);
    
}
#pragma mark -
#pragma mark 形变
//形变
-(void)transform{
    UIView *changeView = [[UIView alloc]initWithFrame:CGRectMake(100, 100, 100, 100)];
    
    UIView *view1 = [[UIView alloc]initWithFrame:CGRectMake(0, 0, 10, 10)];
    [view1 setBackgroundColor:[UIColor blueColor]];
    [changeView addSubview:view1];
   
    changeView.backgroundColor = [UIColor yellowColor];
    
//    平移
    changeView.transform = CGAffineTransformMakeTranslation(0, 100);
//    缩放
//    changeView.transform = CGAffineTransformMakeScale(0.5, 1.0);

//    旋转
//    传入的值为正值时，顺时针转动
    CGFloat angle = [self getAgreeFromDegree:20];
    changeView.transform = CGAffineTransformMakeRotation(angle);
    
    [self.view addSubview:changeView];
}
-(CGFloat)getAgreeFromDegree:(CGFloat)degree{
    CGFloat agree = degree * M_PI / 180;
    return agree;
}
//创建一个UIView
-(void)createUIView{
//    初始化UIView
    UIView *orangeView = [[UIView alloc]init];
//    设置背景色
    orangeView.backgroundColor = [UIColor orangeColor];
//    设置frame
    orangeView.frame = CGRectMake(0, 0, 100, 100);
//    设置center
    orangeView.center = CGPointMake(0, 0);
    orangeView.center = self.view.center;
    
//    添加到视图
    [self.view addSubview:orangeView];
}

@end
```

