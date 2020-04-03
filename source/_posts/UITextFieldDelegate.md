---
title: UITextFieldDelegate
categories:
  - Objective-C
abbrlink: 10117
tags:
  - UITextField
  - UITextFieldDelegate
date: 2017-02-11 56:25:47
---



```objc
#import "RootViewController.h"

@interface RootViewController ()<UITextFieldDelegate>

@end

@implementation RootViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    [self createTextField];
}
//创建UITextField
-(void)createTextField{
//    初始化UITextField
    UITextField *textField = [[UITextField alloc]initWithFrame:CGRectMake(100, 400, 180, 50)];
//    设置背景色
    textField.backgroundColor = [UIColor yellowColor];
//    设置边框样式
    textField.borderStyle = UITextBorderStyleRoundedRect;
    
    
//    一键清除butotn
    textField.clearButtonMode = UITextFieldViewModeWhileEditing;
    
    textField.delegate = self;
    
//    添加到视图
    [self.view addSubview:textField];
}
#pragma mark - delegate

//点击return键，执行的方法
-(BOOL)textFieldShouldReturn:(UITextField *)textField{
    NSLog(@"点击了return");
//    注销第一响应
    [textField resignFirstResponder];
    return YES;
}

//是否能进入编辑
-(BOOL)textFieldShouldBeginEditing:(UITextField *)textField{
    NSLog(@"将要开始编辑");
//    YES:可以进入编辑
//    NO:不能进入编辑
    return YES;
}
//当上面的方法返回YES的时候，才会调用此代理方法
-(void)textFieldDidBeginEditing:(UITextField *)textField{
    NSLog(@"已经开始编辑");
}
//将要结束编辑
-(BOOL)textFieldShouldEndEditing:(UITextField *)textField{
    NSLog(@"将要结束编辑");
    //    YES:可以结束编辑
    //    NO:不能结束编辑
    return YES;
}
//当上面的方法返回YES的时候，才会调用此代理方法
//已经结束编辑
-(void)textFieldDidEndEditing:(UITextField *)textField{
    NSLog(@"已经结束编辑");
}

//点击clearButton时调用的方法
-(BOOL)textFieldShouldClear:(UITextField *)textField{
//    当textField.text值是1的时候，不允许删除
    if ([textField.text isEqualToString:@"1"]) {
        return NO;
    }
//    YES:允许删除
//    NO:不允许删除
    return YES;
}

//获得每一次输入的字符
-(BOOL)textField:(UITextField *)textField shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string{
    
//    NSLog(@"string = %@",string);
    
//    根据每次输入的字符，组成一个字符串
    NSMutableString *mutableString = [[NSMutableString alloc]initWithString:textField.text];
    [mutableString insertString:string atIndex:range.location];
    NSLog(@"%@",mutableString);
    
    return YES;
}
@end

```

