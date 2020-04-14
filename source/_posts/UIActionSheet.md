---
title: UIActionSheet(Objc)
categories:
  - Objective-C
abbrlink: 10130
tags:
  - UIActionSheet
date: 2017-03-19 16:29:10
---

#### UIActionSheet

```objc
#import "ViewController.h"

@interface ViewController ()<UIActionSheetDelegate>

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view, typically from a nib.
}

-(void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event{
//    初始化
    UIActionSheet *sheet = [[UIActionSheet alloc]initWithTitle:@"分享" delegate:self cancelButtonTitle:@"取消" destructiveButtonTitle:@"删除" otherButtonTitles:@"微博分享",@"微信分享",@"QQ分享", nil];
//    显示在指定的view上
    [sheet showInView:self.view];
}
-(void)actionSheet:(UIActionSheet *)actionSheet clickedButtonAtIndex:(NSInteger)buttonIndex{
//    在这里做事件处理
    switch (buttonIndex) {
        case 0:
            NSLog(@"%ld",buttonIndex);
            break;
        case 1:
            NSLog(@"%ld",buttonIndex);
            break;
        case 2:
            NSLog(@"%ld",buttonIndex);
            break;
        case 3:
            NSLog(@"%ld",buttonIndex);
            break;
        case 4:
            NSLog(@"%ld",buttonIndex);
            break;
            
            
        default:
            break;
    }
}
@end

```

