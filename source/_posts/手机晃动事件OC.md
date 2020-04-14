---
title: 手机晃动事件(Objc)
categories:
  - Objective-C
abbrlink: 10119
tags:
  - 手机晃动事件
date: 2017-01-29 14:55:34
---

#### 手机晃动事件

```objc
#define screenWidth self.view.frame.size.width
#define screenHeight self.view.frame.size.height


#import "ViewController.h"

@interface ViewController ()
{
    UIImageView *_topImageView;
    UIImageView *_bottomImageView;
    UIImageView *_showImageView;
}
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    [self createImageViews];
}
//检测到手机晃动
-(void)motionBegan:(UIEventSubtype)motion withEvent:(UIEvent *)event{
//    显示中间的图片
    [self showImageView];
    NSLog(@"晃动开始");
}
//晃动结束
-(void)motionEnded:(UIEventSubtype)motion withEvent:(UIEvent *)event{
//    隐藏中间的图片
    [self hideImageView];
    NSLog(@"晃动结束");
}

-(void)hideImageView{
    [UIView animateWithDuration:2 animations:^{
      //        设置返回原始位置
        _topImageView.frame = CGRectMake(0, 0, screenWidth, screenHeight/2);
        _bottomImageView.frame = CGRectMake(0, screenHeight/2, screenWidth, screenHeight/2);
    }];
}
-(void)showImageView{
//    使用动画为了更美观
    [UIView animateWithDuration:1 animations:^{
        
        _topImageView.frame = CGRectMake(0, -100, screenWidth, screenHeight/2);
        _bottomImageView.frame = CGRectMake(0, screenHeight/2 + 100, screenWidth, screenHeight/2);
    }];
}
#pragma mark 创建UI
-(void)createImageViews{
    
    _showImageView = [[UIImageView alloc]initWithFrame:CGRectMake(0, 0, 150, 150)];
    _showImageView.center = self.view.center;
    _showImageView.image = [UIImage imageNamed:@"ShakeHideImg_women"];
    [self.view addSubview:_showImageView];
    
    
    _topImageView = [[UIImageView alloc]initWithFrame:CGRectMake(0, 0, self.view.frame.size.width, self.view.frame.size.height/2)];
    _topImageView.image = [UIImage imageNamed:@"Shake_Logo_Up"];
    [self.view addSubview:_topImageView];
    
    _bottomImageView = [[UIImageView alloc]initWithFrame:CGRectMake(0, self.view.frame.size.height/2, self.view.frame.size.width, self.view.frame.size.height/2)];
    _bottomImageView.image = [UIImage imageNamed:@"Shake_Logo_Down"];
    [self.view addSubview:_bottomImageView];
}


@end
                                                                    
                                                                    
```

