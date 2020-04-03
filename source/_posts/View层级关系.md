---
title: View切换层级
categories:
  - Objective-C
abbrlink: 10115
tags:
  - Objective-C
  - View层级
date: 2017-02-12 09:47:21
---


#### View切换层级

```objc
#import "RootViewController.h"

@interface RootViewController ()

@end

@implementation RootViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    [self createSubViews];
    
}

-(void)createSubViews{

    UILabel *redLabel = [[UILabel alloc]initWithFrame:CGRectMake(10, 10, 100, 100)];
    redLabel.backgroundColor = [UIColor redColor];
    redLabel.text = @"红色";
    [self.view addSubview:redLabel];
    
    UILabel *greenLabel = [[UILabel alloc]initWithFrame:CGRectMake(50, 50, 100, 100)];
    greenLabel.backgroundColor = [UIColor greenColor];
    greenLabel.text = @"绿色";
    [self.view addSubview:greenLabel];
    
    UILabel *blueLabel = [[UILabel alloc]initWithFrame:CGRectMake(80, 80, 100, 100)];
    blueLabel.backgroundColor = [UIColor blueColor];
    blueLabel.text = @"蓝色";
    [self.view addSubview:blueLabel];
    
//    把子视图提到最前面
//    [self.view bringSubviewToFront:redLabel];
    
//    把子视图放到最底层
//    [self.view sendSubviewToBack:blueLabel];
    
//    把某一个子视图放到第0层
//    [self.view insertSubview:blueLabel atIndex:0];
    
//    把blueLabel 放到greenLabel 下面
//    [self.view insertSubview:blueLabel belowSubview:greenLabel];
    
//    把blueLabel放置到redLabel 上面
//    [self.view insertSubview:redLabel aboveSubview:blueLabel];
    
    NSLog(@"subViews = %@",self.view.subviews);

}

@end

```

