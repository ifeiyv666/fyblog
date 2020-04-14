---
title: NavgationController细化(Objc)
categories:
  - Objective-C
abbrlink: 10127
tags:
  - NavgationController
date: 2017-03-08 11:58:41
---

#### NavgationController细化

```objc
#import "AppDelegate.h"
#import "RootViewController.h"
@interface AppDelegate ()

@end

@implementation AppDelegate


- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    //初始化window
    self.window = [[UIWindow alloc]initWithFrame:[UIScreen mainScreen].bounds];
    //设置背景颜色
    self.window.backgroundColor = [UIColor whiteColor];
    //视图控制器
    RootViewController *rootVC = [[RootViewController alloc]init];
//    初始化导航控制器，并设置基栈
    UINavigationController *nav = [[UINavigationController alloc]initWithRootViewController:rootVC];
    nav.view.backgroundColor = [UIColor redColor];
    
    
    //系统控制器设置为自创的
    self.window.rootViewController = nav;
    
    //让self.window 显示
    [self.window makeKeyAndVisible];
    
    return YES;
}

#import "RootViewController.h"
#import "SecondViewController.h"
@interface RootViewController ()

@end

@implementation RootViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    
    [self.view setBackgroundColor:[UIColor yellowColor]];
    
    UIButton *button = [UIButton buttonWithType:UIButtonTypeCustom];
    button.frame = CGRectMake(100, 100, 100, 50);
    [button setTitle:@"下一级" forState:UIControlStateNormal];
    button.backgroundColor = [UIColor lightGrayColor];
    [button addTarget:self action:@selector(onClick) forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button];
    
    [self settingNavgationBar];
}
-(void)settingNavgationBar{
    
    UINavigationBar *bar = self.navigationController.navigationBar;
    
//    设置navigationBar 的类型
    self.navigationController.navigationBar.barStyle = UIBarStyleBlack;
//    UIBarStyleDefault
//    UIBarStyleBlack
    
//    透明度(毛玻璃)
    bar.translucent = YES;
//    设置yes，子视图的坐标原点是（0,0）
//    设置no,子视图的坐标原点是(0,64)
    UILabel *label = [[UILabel alloc]initWithFrame:CGRectMake(0, 0, 100, 100)];
    label.backgroundColor = [UIColor greenColor];
    [self.view addSubview:label];
    
//    设置导航条颜色
    [bar setBarTintColor:[UIColor redColor]];
    
//    设置标题
//    self.title = @"root";
    self.navigationItem.title = @"root";
    
//    导航条按钮字体颜色
    [bar setTintColor:[UIColor cyanColor]];
    
//    设置导航条字体颜色
    [bar setTitleTextAttributes:@{
                                 NSFontAttributeName:[UIFont systemFontOfSize:20],
                                 NSForegroundColorAttributeName:[UIColor purpleColor]
                                 }];
    
//    设置隐藏导航条
//    self.navigationController.navigationBarHidden = YES;
    
    [bar setBackgroundImage:[UIImage imageNamed:@"header_bg44"] forBarMetrics:UIBarMetricsDefault];
//    UIBarMetricsDefault 横竖屏都显示
//    UIBarMetricsCompact 竖屏显示
    
    
//    self.navigationItem.backBarButtonItem = [[UIBarButtonItem alloc]initWithTitle:@"返回" style:UIBarButtonItemStylePlain target:secondVc     action:@selector(abc)];
    
    UIImage *image = [UIImage imageNamed:@"qq.png"];
//    对图片进处理
   image =  [image imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
    
//    UIImageRenderingModeAutomatic,返回一个色块
//    UIImageRenderingModeAlwaysOriginal,返回图片本身       UIImageRenderingModeAlwaysTemplate,返回一个色块
    
//    UIBarButtonItemStylePlain,
//    UIBarButtonItemStyleDone,
    
//    leftBarButtonItem 左按钮
    self.navigationItem.leftBarButtonItem = [[UIBarButtonItem alloc]initWithImage:image style:UIBarButtonItemStylePlain target:self     action:@selector(leftClick)];
//    rightBarButtonItem 右按钮
    self.navigationItem.rightBarButtonItem = [[UIBarButtonItem alloc]initWithTitle:@"right" style:UIBarButtonItemStyleDone target:self action:@selector(rightClick)];
    
    UIBarButtonItem *item1 = [[UIBarButtonItem alloc]initWithTitle:@"item1" style:UIBarButtonItemStylePlain target:self action:@selector(rightClick)];
    
    UIBarButtonItem *item2 = [[UIBarButtonItem alloc]initWithTitle:@"item2" style:UIBarButtonItemStylePlain target:self action:@selector(rightClick)];
    

    
    UIButton *button = [UIButton buttonWithType:UIButtonTypeCustom];
    button.frame = CGRectMake(0, 0, 40, 40);
    [button setBackgroundColor:[UIColor redColor]];
    
    [button setImage:image forState:UIControlStateNormal];
    
//    添加一个自定义的UIButton
    UIBarButtonItem * item3 = [[UIBarButtonItem alloc]initWithCustomView:button];
    
    //    设置rightBarButtonItems时，会把rightBarButtonItem 覆盖
    self.navigationItem.rightBarButtonItems = @[item1,item2,item3];
    
    UILabel *label1 = [[UILabel alloc]initWithFrame:CGRectMake(0, 0, 100, 44)];
    label1.backgroundColor = [UIColor redColor];
    label1.text = @"label";
    
    UIImageView *imageView = [[UIImageView alloc]initWithFrame:CGRectMake(0, 0, 100, 40)];
    imageView.image = image;
//    设置titleView
    self.navigationItem.titleView = imageView;
    
}
-(void)leftClick{
    NSLog(@"---");
}
-(void)rightClick{
    NSLog(@"%s",__func__);
}
-(void)onClick{
    
    SecondViewController *secondVc = [[SecondViewController alloc]init];
//    进入下一级（入栈）
    [self.navigationController pushViewController:secondVc animated:YES];
    
    
}
@end


#import "SecondViewController.h"
#import "ThirdViewController.h"
@interface SecondViewController ()

@end

@implementation SecondViewController
-(void)viewWillAppear:(BOOL)animated{
    [super viewWillAppear:animated];
//    视图将要出现的时候，隐藏navgationBar
        self.navigationController.navigationBarHidden = YES;
}
-(void)viewWillDisappear:(BOOL)animated{
    [super viewWillDisappear:animated];
//    视图将要消失的时候，显示navgationBar
    self.navigationController.navigationBarHidden = NO;
}
- (void)viewDidLoad {
    [super viewDidLoad];
    

    
    [self.view setBackgroundColor:[UIColor greenColor]];
    
    UIButton *button = [UIButton buttonWithType:UIButtonTypeCustom];
    button.frame = CGRectMake(100, 100, 100, 50);
    [button setTitle:@"下一级" forState:UIControlStateNormal];
    button.backgroundColor = [UIColor lightGrayColor];
    [button addTarget:self action:@selector(onClick) forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button];
    
    UIButton *button1 = [UIButton buttonWithType:UIButtonTypeCustom];
    button1.frame = CGRectMake(100, 200, 100, 50);
    [button1 setTitle:@"上一级" forState:UIControlStateNormal];
    button1.backgroundColor = [UIColor lightGrayColor];
    [button1 addTarget:self action:@selector(backClick) forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button1];
}

-(void)abc{
    NSLog(@"----");
}
-(void)backClick{
//    返回上一级
    [self.navigationController popViewControllerAnimated:YES];
}
-(void)onClick{
    ThirdViewController *thirdVc = [[ThirdViewController alloc]init];
//    进入下一级（入栈）
    [self.navigationController pushViewController:thirdVc animated:YES];
    
    
}
- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}


@end

#import "ThirdViewController.h"
#import "ForthViewController.h"
@interface ThirdViewController ()

@end

@implementation ThirdViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    
    [self.view setBackgroundColor:[UIColor blueColor]];
    
    for (int i = 0 ; i < 3; i ++) {
        
        UIButton *button = [UIButton buttonWithType:UIButtonTypeCustom];
        button.frame = CGRectMake(100, 100 + i * 60, 100, 50);
        button.tag = i + 10;
        if (i == 0 ) {
           [button setTitle:@"下一级" forState:UIControlStateNormal];
        }else if (i == 1){
            [button setTitle:@"上一级" forState:UIControlStateNormal];
        }else if (i == 2){
            [button setTitle:@"返回root" forState:UIControlStateNormal];
        }
        
        button.backgroundColor = [UIColor lightGrayColor];
        [button addTarget:self action:@selector(onClick:) forControlEvents:UIControlEventTouchUpInside];
        [self.view addSubview:button];

        
    }
    
//    self.navigationController.viewControllers
    NSLog(@"%@",self.navigationController.viewControllers);
    
    [self toolBarSetting];
}

-(void)toolBarSetting{
    self.navigationController.toolbarHidden = NO;
    
    UIBarButtonItem *item = [[UIBarButtonItem alloc]initWithBarButtonSystemItem:UIBarButtonSystemItemSave target:nil action:nil];
    
    UIBarButtonItem *item1 = [[UIBarButtonItem alloc]initWithBarButtonSystemItem:UIBarButtonSystemItemAdd target:nil action:nil];
    
    UIBarButtonItem *item2 = [[UIBarButtonItem alloc]initWithBarButtonSystemItem:UIBarButtonSystemItemEdit target:nil action:nil];
    
    UIBarButtonItem *item3 = [[UIBarButtonItem alloc]initWithBarButtonSystemItem:UIBarButtonSystemItemFlexibleSpace target:nil action:nil];
    
    
    self.toolbarItems = @[item,item3,item1,item2];
    
}
-(void)onClick:(UIButton*)button{
    if (button.tag == 10) {
        ForthViewController *forthVc = [[ForthViewController alloc]init];
//       把forthVc 入栈
        [self.navigationController pushViewController:forthVc animated:YES];
    }
    if (button.tag == 11) {
//        返回上一级
        [self.navigationController popViewControllerAnimated:YES];
    }
    if (button.tag == 12) {
//        返回root(基栈)
        [self.navigationController popToRootViewControllerAnimated:YES];
    }
}


@end

#import "ForthViewController.h"

@interface ForthViewController ()

@end

@implementation ForthViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.
//    设置背景色
    [self.view setBackgroundColor:[UIColor orangeColor]];
//    初始化button
    for (int i = 0 ; i < 3; i ++) {
        
        UIButton *button = [UIButton buttonWithType:UIButtonTypeCustom];
        button.frame = CGRectMake(100, 100 + i * 60, 100, 50);
        button.tag = i + 10;
        if (i == 0 ) {
            [button setTitle:@"返回第二级" forState:UIControlStateNormal];
        }else if (i == 1){
            [button setTitle:@"上一级" forState:UIControlStateNormal];
        }else if (i == 2){
            [button setTitle:@"返回root" forState:UIControlStateNormal];
        }
        
        button.backgroundColor = [UIColor lightGrayColor];
        [button addTarget:self action:@selector(onClick:) forControlEvents:UIControlEventTouchUpInside];
        [self.view addSubview:button];
        
        
    }
    
}
-(void)onClick:(UIButton*)button{
    if (button.tag == 10) {
//       根据数组下标 获取要返回到的UIViewController
        UIViewController *VC =   self.navigationController.viewControllers[1];
//        返回到指定的UIViewController
        [self.navigationController popToViewController:VC animated:YES];
    }
    if (button.tag == 11) {
//        返回上一级
        [self.navigationController popViewControllerAnimated:YES];
    }
    if (button.tag == 12) {
//        返回到root(基栈)
        [self.navigationController popToRootViewControllerAnimated:YES];
    }
}
@end


```

