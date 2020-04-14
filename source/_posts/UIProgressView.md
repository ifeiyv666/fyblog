---
title: UIProgressView(Objc)
categories:
  - Objective-C
abbrlink: 10135
tags:
  - UIProgressView
date: 2017-03-06 15:24:55
---

#### UIProgressView

```objc

#import "ViewController.h"

@interface ViewController ()
{
    NSTimer *_timer;
}
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
// 初始化UIProgressView并设置frame
//    UIProgressView 高度是固定的
    UIProgressView *progressView = [[UIProgressView alloc]initWithFrame:CGRectMake(100, 100, 200, 100)];
//    设置进度
//    0.0 .. 1.0, default is 0.0.
    progressView.progress = 0.25;
//    已加载进度的颜色
    progressView.progressTintColor = [UIColor redColor];
//    未加载进度的颜色
    progressView.trackTintColor = [UIColor greenColor];
//    设置图片会覆盖上面设置的颜色
//    已加载进度的图片
    progressView.progressImage = [UIImage imageNamed:@"1"];
//    未加载进度的图片
    progressView.trackImage = [UIImage imageNamed:@"2"];
    
//    设置tag值
    progressView.tag = 10;
    
//    添加到视图
    [self.view addSubview:progressView];
    
//    初始化timer
    _timer = [NSTimer     scheduledTimerWithTimeInterval:0.1 target:self selector:@selector(timerRun) userInfo:nil repeats:YES];
    
}
-(void)timerRun{
    UIProgressView *progressView = (UIProgressView *)[self.view viewWithTag:10];
    
    if (progressView.progress < 1.0) {
        progressView.progress += 0.01;
    }else{
        NSLog(@"下载完成");
//        使计时器失效
        [_timer invalidate];
    }
    
}
@end

```

