---
title: Touch(Objc)
categories:
  - Objective-C
abbrlink: 10128
tags:
  - Touch
date: 2017-03-14 15:37:51
---

#### Touch

```objc
#import "ViewController.h"

@interface ViewController ()
{
    UIView *myview;
}
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
//    初始化myview
    myview = [[UIView alloc]initWithFrame:CGRectMake(100,100, 100, 100)];
//    设置背景色
    myview.backgroundColor = [UIColor lightGrayColor];
//    添加到视图上
    [self.view addSubview:myview];
    
}
//开始触摸，只调用一次
-(void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event{
    NSLog(@"touch began");
}
//开始移动，会多次调用
-(void)touchesMoved:(NSSet *)touches withEvent:(UIEvent *)event{
    NSLog(@"----");
//    UITouch
//    用来保存跟手指相关的信息，比如：触摸的位置
//    当手指移动时，系统会更新同一个UIToch对象，使之能够一直保存该手指在的触摸位置
//    当手指离开屏幕时，系统会销毁对应的UITouch对象
//
//    从touches中取出手指
    UITouch *touch = [touches anyObject];
    
    if (touch.view == myview) {
        
        //    该方法记录了前一个触摸点的位置
        CGPoint previousPoint = [touch previousLocationInView:self.view];
        
        /*
         返回值表示触摸在self.view上的位置
         这里的位置是针对self.view的坐标系（以self.view的左上角为原点（0,0））
         如果传nil时，返回的触摸点在UIWindow的位置
         */
        
        //    该方法记录了当前点的位置
        CGPoint currentPoint = [touch locationInView:self.view];
        
        NSLog(@"1------>%@",NSStringFromCGPoint(previousPoint));
        NSLog(@"2------>%@",NSStringFromCGPoint(currentPoint));
        //    获取x偏移量
        CGFloat x = currentPoint.x - previousPoint.x;
        //    获取y偏移量
        CGFloat y = currentPoint.y - previousPoint.y;
        
        //    获取myview中心点
        CGPoint center = myview.center;
        
        center.x += x;
        center.y += y;
        
        myview.center = center;
    }
}
//结束触摸，只调用一次
-(void)touchesEnded:(NSSet *)touches withEvent:(UIEvent *)event{
    NSLog(@"touch end");
}
//触摸取消（例如来电打断）
-(void)touchesCancelled:(NSSet *)touches withEvent:(UIEvent *)event{
    
}
@end

```

