---
title: UIAlertController(Objc)
categories:
  - Objective-C
abbrlink: 10131
tags:
  - UIAlertController
date: 2017-02-23 11:45:09
---

#### UIAlertController

```objc

#import "ViewController.h"

@interface ViewController ()

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    for (int i = 0 ; i < 2; i ++) {
        UIButton *button =[UIButton buttonWithType:UIButtonTypeCustom];
        button.frame = CGRectMake(120 + i * 120, 120, 100, 50);
        button.backgroundColor = [UIColor lightGrayColor];
        if (i == 0) {
            [button setTitle:@"alertView" forState:UIControlStateNormal];
        }else{
            [button setTitle:@"actionSheet" forState:UIControlStateNormal];
        }
        button.tag = 10 + i ;
        [button addTarget:self action:@selector(onClick:) forControlEvents:UIControlEventTouchUpInside];
        
        [self.view addSubview:button];
    }
    
}
-(void)onClick:(UIButton*)button{
    
    if (button.tag == 10) {
        NSLog(@"alertView");
        [self alertView];
    }else{
        NSLog(@"actionSheet");
        [self actionSheet];
    }
}
-(void)actionSheet{
//    初始化UIAlertCOntroller
//    Title:标题
//    message:信息
//    Style:样式
    UIAlertController *alertController = [UIAlertController alertControllerWithTitle:@"提示" message:@"message" preferredStyle:UIAlertControllerStyleActionSheet];
    
//    初始化UIAlertAction
    UIAlertAction *cancelBtn = [UIAlertAction actionWithTitle:@"取消" style:UIAlertActionStyleCancel handler:^(UIAlertAction *  action) {
        NSLog(@"取消");
    }];
    
    UIAlertAction *firstBtn = [UIAlertAction actionWithTitle:@"first" style:UIAlertActionStyleDefault handler:^(UIAlertAction * action) {
        NSLog(@"取消");
    }];
    
    
    
    [alertController addAction:cancelBtn];
    [alertController addAction:firstBtn];
    [self presentViewController:alertController animated:YES completion:nil];
    
}
-(void)alertView{
//    初始化UIAlertController
//    Title:标题
//    message:信息
//    Style:样式
    UIAlertController *alertController = [UIAlertController alertControllerWithTitle:@"提示" message:@"message" preferredStyle:UIAlertControllerStyleAlert];
//    UIAlertControllerStyleActionSheet
//    UIAlertControllerStyleAlert
    
//    初始化按钮
//    Title：标题
//    style：样式
//    UIAlertController 上面只能有一个取消样式的按钮，否则会崩溃
    UIAlertAction *cancelBtn = [UIAlertAction actionWithTitle:@"取消" style:UIAlertActionStyleCancel handler:^(UIAlertAction *  action) {
        NSLog(@"取消");
    }];
//    UIAlertActionStyleDefault = 0,普通按钮
//    UIAlertActionStyleCancel,取消按钮
//    UIAlertActionStyleDestructive重置、销毁

//    添加文本输入框
    [alertController addTextFieldWithConfigurationHandler:^(UITextField *  textField) {
        textField.placeholder = @"请输入";
    }];
    
    [alertController addTextFieldWithConfigurationHandler:^(UITextField * textField) {
        textField.placeholder = @"第二个文本输入框";
    }];
    
    UIAlertAction *resetBtn = [UIAlertAction actionWithTitle:@"reset" style:UIAlertActionStyleDestructive handler:^(UIAlertAction *  action) {
        
        UITextField *textField1 = alertController.textFields[0];
        NSLog(@"%@",textField1.text);
        
        UITextField *textField2 = alertController.textFields[1];
        NSLog(@"%@",textField2.text);
    }];
    
    
//    添加动作
    [alertController addAction:cancelBtn];
    [alertController addAction:resetBtn];
    
    
//    模态
    [self presentViewController:alertController animated:YES completion:nil];
}
@end

```

