---
title: UIActivityIndicatorView(Objc)
categories:
  - Objective-C
abbrlink: 10131
tags:
  - UIActivityIndicatorView
date: 2017-02-22 10:58:06
---

#### UIActivityIndicatorView

```objc
#import "myButton.h"

@implementation myButton

+(UIButton *)buttonWithFrame:(CGRect)frame BGColor:(UIColor *)color Title:(NSString *)title NormalImage:(UIImage *)normalImage Tag:(int)tag Method:(SEL)method Object:(id)object{
    UIButton *button = [UIButton buttonWithType:UIButtonTypeCustom];
    button.frame = frame;
    button.backgroundColor = color;
    [button setTitle:title forState:UIControlStateNormal];
    button.tag = tag;
    [button setBackgroundImage:normalImage forState:UIControlStateNormal];
    [button addTarget:object action:method forControlEvents:UIControlEventTouchUpInside];
    return button;
}

@end


#import "ViewController.h"
#import "myButton.h"
@interface ViewController ()
{
    UIActivityIndicatorView *act;
}
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    
    [self createBtn];
    [self createActivityIndicatorView];
}
-(void)onClick:(UIButton*)button{
    if (act.isAnimating == YES) {
        [act stopAnimating];
    }else if(act.isAnimating == NO){
        [act startAnimating];
    }
    
}
-(void)createActivityIndicatorView{
    
//    UIActivityIndicatorViewStyleWhiteLarge,大白
//    UIActivityIndicatorViewStyleWhite,白色
//    UIActivityIndicatorViewStyleGray 灰色
//    初始化并设置样式
    act = [[UIActivityIndicatorView alloc]initWithActivityIndicatorStyle:UIActivityIndicatorViewStyleGray];
    act.frame = CGRectMake(100, 300, 50, 50);
//    设置中心点为屏幕中心点
    act.center = self.view.center;
    [self.view addSubview:act];
    
    act.backgroundColor = [UIColor redColor];
    
//    设置变大4倍
    act.transform = CGAffineTransformMakeScale(4, 4);
    
    act.tag = 10;
//    停止时是否隐藏，默认是YES
    act.hidesWhenStopped = YES;
}
-(void)createBtn{
    UIButton *startBtn = [myButton buttonWithFrame:CGRectMake(100, 100, 50, 50) BGColor:[UIColor lightGrayColor] Title:@"开始" NormalImage:nil Tag:10 Method:@selector(onClick:) Object:self];
    
    [self.view addSubview:startBtn];
    
    UIButton *endBtn = [myButton buttonWithFrame:CGRectMake(180, 100, 50, 50) BGColor:[UIColor lightGrayColor] Title:@"停止" NormalImage:nil Tag:11 Method:@selector(onClick:) Object:self];
    [self.view addSubview:endBtn];
    
    [self.view setBackgroundColor:[UIColor yellowColor]];
}
@end

```

