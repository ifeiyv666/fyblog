---
title: UIImageView(Objc)
categories:
  - Objective-C
abbrlink: 10133
tags:
  - UIImageView
date: 2017-03-01 16:34:56
---

#### UIImageView

```objc
#import "RootViewController.h"

@interface RootViewController ()

@end

@implementation RootViewController

- (void)viewDidLoad {
    [super viewDidLoad];

//    [self createUIImageView];
    [self UIImageViewAnimation];
}

-(void)UIImageViewAnimation{
    UIImageView *bgView = [[UIImageView alloc]initWithFrame:self.view.bounds];
    bgView.image = [UIImage imageNamed:@"back2.jpg"];
    [self.view addSubview:bgView];
    
    UIImageView *birdView = [[UIImageView alloc]initWithFrame:CGRectMake(100, 100, 121, 96)];
    birdView.image = [UIImage imageNamed:@"DOVE 1"];
    
    NSMutableArray *mArray = [NSMutableArray array];
    for (int i = 1 ; i <19; i ++) {
        NSString *PicName = [NSString stringWithFormat:@"DOVE %d",i];
        UIImage *image = [UIImage imageNamed:PicName];
        [mArray addObject:image];
    }
    
    birdView.animationImages = mArray;
    birdView.animationDuration = 1;
    birdView.animationRepeatCount = 2;
    [birdView startAnimating];
    
    [self.view addSubview:birdView];
    
}

//创建UIImageView
-(void)createUIImageView{
    /*
    UIImageView *imageView = [[UIImageView alloc]initWithImage:[UIImage imageNamed:@"back2.jpg"]];
    [self.view addSubview:imageView];
     */
    UIImageView *imageView = [[UIImageView alloc]initWithFrame:CGRectMake(50, 50, 200, 200)];
    imageView.backgroundColor = [UIColor lightGrayColor];
    imageView.image = [UIImage imageNamed:@"back2.jpg"];
    imageView.contentMode = UIViewContentModeScaleAspectFill;
//    UIViewContentModeScaleToFill
//    UIViewContentModeScaleAspectFit
//    UIViewContentModeScaleAspectFill
    [self.view addSubview:imageView];
    

    
//UIImage在初始化图片时，能获得图片的size
    UIImage *image = [UIImage imageNamed:@"back2.jpg"];
    NSLog(@"%f----%f",image.size.width,image.size.height);
}

@end

```

