---
title: delegate反向传值
categories:
  - Objective-C
abbrlink: 10116
tags:
  - delegate
  - delegate反向传值
date: 2017-01-26 36:17:29
---

#### delegate反向传值

```objc
#import "RootViewController.h"
#import "SecondViewController.h"
@interface RootViewController ()<SecondViewControllerDelegate>

@end
@implementation RootViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    [self createButton];
}
-(void)createButton{
    UIButton *button = [UIButton buttonWithType:UIButtonTypeCustom];
    button.frame = CGRectMake(100, 100, 100, 100);
    button.backgroundColor = [UIColor lightGrayColor];
    [button setTitle:@"下一页" forState:UIControlStateNormal];
    [button addTarget:self action:@selector(onClick) forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button];
}
-(void)onClick{
    SecondViewController *secondVc = [[SecondViewController alloc]init];
    secondVc.delegate = self;
    [self.navigationController pushViewController:secondVc animated:YES];
}

-(void)changeColor:(UIColor *)color{
    [self.view setBackgroundColor:color];
}

@end
  
  
```



```objc
#import "SecondViewController.h"

@interface SecondViewController ()

@end

@implementation SecondViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.
    [self createButton];
    
    [self.view setBackgroundColor:[UIColor lightGrayColor]];
}
-(void)createButton{
    UIButton *button = [UIButton buttonWithType:UIButtonTypeCustom];
    button.frame = CGRectMake(100, 100, 100, 100);
    button.backgroundColor = [UIColor lightGrayColor];
    [button setTitle:@"上一页" forState:UIControlStateNormal];
    [button addTarget:self action:@selector(onClick) forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button];
}
-(void)onClick{
    if (self.delegate && [self.delegate respondsToSelector:@selector(changeColor:)]) {
        [self.delegate changeColor:[UIColor yellowColor]];
    }
    [self.navigationController popViewControllerAnimated:YES];
}
@end

```

