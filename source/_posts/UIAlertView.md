---
title: UIAlertView(Objc)
categories:
  - Objective-C
abbrlink: 10132
tags:
  - UIAlertView
date: 2017-02-25 09:39:42
---

#### UIAlertView

```objc

#import "ViewController.h"

@interface ViewController ()<UIAlertViewDelegate>
{
    int number;
}
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    
}
//点击屏幕就会触发此方法
-(void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event{
    number = arc4random()%2;
    NSLog(@"number = %d",number);
    if (number == 0) {
        UIAlertView *alert = [[UIAlertView alloc]initWithTitle:@"提示" message:@"赶快还钱" delegate:self cancelButtonTitle:@"还钱" otherButtonTitles:@"不还",@"就不还", nil];
        [alert show];
    }
    if (number == 1) {
        UIAlertView *alert = [[UIAlertView alloc]initWithTitle:@"提示" message:@"还钱" delegate:self cancelButtonTitle:@"还钱" otherButtonTitles:@"不还",@"就不还", nil];
        
        
        alert.alertViewStyle = UIAlertViewStyleLoginAndPasswordInput;
        
        [alert show];
        
//        UIAlertViewStyleDefault = 0,
//        UIAlertViewStyleSecureTextInput,
//        UIAlertViewStylePlainTextInput,
//        UIAlertViewStyleLoginAndPasswordInput
    }
}
#pragma mark -
#pragma mark delegate
-(void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex{
    if (number == 0) {
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
                
            default:
                break;
        }

    }else{

        switch (buttonIndex) {
            case 0:
                NSLog(@"%ld",buttonIndex);        NSLog(@"%@",[[alertView textFieldAtIndex:0]text]);
                NSLog(@"%@",[[alertView textFieldAtIndex:1]text]);
                break;
            case 1:
                NSLog(@"%ld",buttonIndex);
                break;
            case 2:
                NSLog(@"%ld",buttonIndex);
                break;
                
            default:
                break;
        }
    }
    
    
}
@end
```

