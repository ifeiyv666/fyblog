---
title: UITableBarController(Objc)
categories:
  - Objective-C
abbrlink: 10140
tags:
  - UITableBarController
date: 2017-04-10 19:23:45
---

#### UITableBarController

```objc
#import "AppDelegate.h"
#import "RootViewController.h"
#import "ViewController1.h"
#import "ViewController2.h"
#import "ViewController3.h"
#import "ViewController4.h"
#import "ViewController5.h"
#import "ViewController6.h"
@interface AppDelegate ()<UITabBarControllerDelegate>
@end
/**
 系统代理的使用：
 1.遵守协议
 2.设置代理
 3.实现代理方法
 */
@implementation AppDelegate


- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    self.window = [[UIWindow alloc]initWithFrame:[UIScreen mainScreen].bounds];
    [self.window setBackgroundColor:[UIColor whiteColor]];
    
    [self createTabBarController];
    
    [self.window makeKeyAndVisible];
    return YES;
}
//创建UITabBarController
-(void)createTabBarController{
//    初始化UITabBarController
    UITabBarController *tabBarVc = [[UITabBarController alloc]init];
    
//    设置代理
    tabBarVc.delegate = self;
    
    self.window.rootViewController = tabBarVc;
    
//    设置tabBar的背景色
//    tabBarVc.tabBar.barTintColor = [UIColor yellowColor];
    
    ViewController1 *vc1 = [[ViewController1 alloc]init];
    ViewController2 *vc2 = [[ViewController2 alloc]init];
    ViewController3 *vc3 = [[ViewController3 alloc]init];
    ViewController4 *vc4 = [[ViewController4 alloc]init];
    ViewController5 *vc5 = [[ViewController5 alloc]init];
    ViewController6 *vc6 = [[ViewController6 alloc]init];
     
//    系统item样式
//    UITabBarSystemItemMore,
//    UITabBarSystemItemFavorites,
//    UITabBarSystemItemFeatured,
//    UITabBarSystemItemTopRated,
//    UITabBarSystemItemRecents,
//    UITabBarSystemItemContacts,
//    UITabBarSystemItemHistory,
//    UITabBarSystemItemBookmarks,
//    UITabBarSystemItemSearch,
//    UITabBarSystemItemDownloads,
//    UITabBarSystemItemMostRecent,
//    UITabBarSystemItemMostViewed,

    
    UITabBarItem *item1 = [[UITabBarItem alloc]initWithTabBarSystemItem:UITabBarSystemItemFavorites tag:11];
    vc1.tabBarItem = item1;
    
    UITabBarItem *item2 = [[UITabBarItem alloc]initWithTabBarSystemItem:UITabBarSystemItemContacts tag:12];
    vc2.tabBarItem = item2;
    
    UITabBarItem *item3 = [[UITabBarItem alloc]initWithTabBarSystemItem:UITabBarSystemItemDownloads tag:13];
    vc3.tabBarItem = item3;
    
    UITabBarItem *item4 = [[UITabBarItem alloc]initWithTabBarSystemItem:UITabBarSystemItemFavorites tag:14];
    vc4.tabBarItem = item4;
    
    UITabBarItem *item5 = [[UITabBarItem alloc]initWithTabBarSystemItem:UITabBarSystemItemFeatured tag:15];
    vc5.tabBarItem = item5;
    
    UITabBarItem *item6 = [[UITabBarItem alloc]initWithTabBarSystemItem:UITabBarSystemItemHistory tag:16];
    vc6.tabBarItem = item6;
    
//    镂空处颜色
    tabBarVc.tabBar.tintColor = [UIColor redColor];
    
//    透明度
    tabBarVc.tabBar.translucent = NO;
    
//    最多只显示5个，多出来的会自动生成一个More，它是一个导航控制器
    tabBarVc.viewControllers = @[vc1,vc2,vc3,vc4,vc5,vc6];
    
//    设置选中哪一个控制器
//    tabBarVc.selectedIndex = 3;
    
    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
    NSUInteger index = [defaults integerForKey:@"index"];
    NSLog(@"%ld",index);
//     设置选中第index个控制器
    tabBarVc.selectedIndex = index;
    
//    排序
    [self order];
}
#pragma mark - 
#pragma mark UITabBarController delegate
-(BOOL)tabBarController:(UITabBarController *)tabBarController shouldSelectViewController:(UIViewController *)viewController{
    NSLog(@"将要选中视图控制器");
    if (viewController.tabBarItem.tag == 13) {
        return NO;
    }
//  YES:可以选中
//  NO:不能选中
    return YES;
}
-(void)tabBarController:(UITabBarController *)tabBarController didSelectViewController:(UIViewController *)viewController{
    NSLog(@"已经选中指定的视图控制器");
    
    NSArray *array = tabBarController.viewControllers;
    NSLog(@"array = %@",array);
    NSUInteger index = [array indexOfObject:viewController];
    
//    初始化NSUserDefaults (单例)
    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
//    设置index
    [defaults setInteger:index forKey:@"index"];
//    同步
    [defaults synchronize];
}
-(void)tabBarController:(UITabBarController *)tabBarController willBeginCustomizingViewControllers:(NSArray *)viewControllers{
    NSLog(@"willBeginCustomizingViewControllers");
}
-(void)tabBarController:(UITabBarController *)tabBarController willEndCustomizingViewControllers:(NSArray *)viewControllers changed:(BOOL)changed{
    NSLog(@"willEndCustomizingViewControllers");
}
-(void)tabBarController:(UITabBarController *)tabBarController didEndCustomizingViewControllers:(NSArray *)viewControllers changed:(BOOL)changed{
    NSLog(@"didEndCustomizingViewControllers");
    
    NSMutableArray *array = [NSMutableArray array];
//    changed用来判断是否交换
    if (changed == YES) {
        for (UIViewController *vc in viewControllers) {
            [array addObject:vc.title];
        }
    }
    NSLog(@"%@",array);
    
    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
    [defaults setObject:array forKey:@"order"];
    [defaults synchronize];
}

-(void)order{
    
    //    获取UITabBarController
    UITabBarController * tbc = (UITabBarController*)self.window.rootViewController;
    
    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
    //    取得之前排序的数组
    NSMutableArray *titleArray = [defaults objectForKey:@"order"];
    
    //    如果排序的数组是nil,返回
    if (titleArray == nil) {
        return;
    }
    
    NSMutableArray *orderArray = [NSMutableArray array];
    for (NSString *titler in titleArray) {
        for (UIViewController *vc  in tbc.viewControllers) {
            if ([titler isEqualToString:vc.title]) {
                [orderArray addObject:vc];
                break;
            }
        }
    }
    tbc.viewControllers = orderArray;
}

@end


#import "BaseViewController.h"

@interface BaseViewController ()

@end

@implementation BaseViewController
-(instancetype)initWithNibName:(NSString *)nibNameOrNil bundle:(NSBundle *)nibBundleOrNil{
    self = [super initWithNibName:nibNameOrNil bundle:nibBundleOrNil];
    if (self) {
        self.title = NSStringFromClass([self class]);
    }
    return self;
}
- (void)viewDidLoad {
    [super viewDidLoad];

#define Random arc4random()%256/255.0
    
    self.view.backgroundColor = [UIColor colorWithRed:Random green:Random blue:Random alpha:0.9f];
    
    UILabel *label = [[UILabel alloc]initWithFrame:CGRectMake(100, 100, 200, 100)];
    NSString *name = NSStringFromClass([self class]);
    label.text = name;
    
    [self.view addSubview:label];
}
@end


```





```objc
#import "AppDelegate.h"
#import "ViewController1.h"
#import "ViewController2.h"
#import "ViewController3.h"
#import "ViewController4.h"
#import "ViewController4_1.h"
@interface AppDelegate ()

@end

@implementation AppDelegate


- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    self.window = [[UIWindow alloc]initWithFrame:[UIScreen mainScreen].bounds];
    [self.window setBackgroundColor:[UIColor whiteColor]];
    
    [self createUITabBarController];
    [self customTabBar];
    
    
    [self.window makeKeyAndVisible];
    
    return YES;
}
//创建UITabBarController
-(void)createUITabBarController{
//    初始化UITabBarController
    UITabBarController *tabBarVc = [[UITabBarController alloc]init];
    self.window.rootViewController = tabBarVc;
    
    
    ViewController1 *vc1 = [[ViewController1 alloc]init];
    ViewController2 *vc2 = [[ViewController2 alloc]init];
    ViewController3 *vc3 = [[ViewController3 alloc]init];
    
    ViewController4 *vc4 = [[ViewController4 alloc]init];
    UINavigationController *nav = [[UINavigationController alloc]initWithRootViewController:vc4];

//    把导航控制器放到分栏控制器中
//    tabBarVc.viewControllers = @[vc1,vc2,vc3,nav];
    
//    初始化UITabBarItem
//    Title：名字
//    image：图片
//    tag:标识
    UITabBarItem *item1 = [[UITabBarItem alloc]initWithTitle:@"微信" image:[UIImage imageNamed:@"tabbar_mainframe" ] tag:11];
    vc1.tabBarItem = item1;
    
    UIImage *image2 = [UIImage imageNamed:@"tabbar_contactsHL"];
//    对图片进行处理(显示原有尺寸)
    image2 = [image2 imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
//
//Title：名称
//image：正常状态image
//selectedImage:选中状态image(需要对图片进行处理，否则会不显示选中图片)
    UITabBarItem *item2 = [[UITabBarItem alloc]initWithTitle:@"通讯录" image:[UIImage imageNamed:@"tabbar_contacts"] selectedImage:image2];
    vc2.tabBarItem = item2;
    
    UIImage *image3 = [UIImage imageNamed:@"tabbar_discoverHL"];
    image3 = [image3 imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
    UITabBarItem *item3 = [[UITabBarItem alloc]initWithTitle:@"朋友圈" image:[UIImage imageNamed:@"tabbar_discover"] selectedImage:image3];
    vc3.tabBarItem = item3;
    
    item3.badgeValue = @"99+";
    
    
    UIImage *image4 = [UIImage imageNamed:@"tabbar_meHL"];
    image4 = [image4 imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
    
    UITabBarItem *item4 = [[UITabBarItem alloc]initWithTitle:@"我" image:[UIImage imageNamed:@"tabbar_me"] selectedImage:image4];
    vc4.tabBarItem = item4;
    
    tabBarVc.viewControllers = @[vc1,vc2,vc3,nav];
}
//设置TabBar
-(void)customTabBar{
//    获取UITabBarController
    UITabBarController *tabBarVc = (UITabBarController*)self.window.rootViewController;
    
//    获取UITabBar
    UITabBar *tabBar = tabBarVc.tabBar;
    
//    设置tabBar样式
    tabBar.barStyle = UIBarStyleDefault;
//    UIBarStyleDefault
//    UIBarStyleBlack
    
//    设置透明度
    tabBar.translucent = YES;
    
//    设置镂空颜色（字体颜色）
    [tabBar setTintColor:[UIColor colorWithRed:0/255.0 green:176/255.0 blue:15/255.0 alpha:1.0]];
    
//    设置tabBar背景色
    [tabBar setBarTintColor:[UIColor redColor]];
    
//    设置背景图片（当设置背景图片时，会覆盖背景色）
    [tabBar setBackgroundImage:[UIImage imageNamed:@"tabbar_bg"]];
    
}

@end


#import "BaseViewController.h"

@interface BaseViewController ()

@end

@implementation BaseViewController
-(instancetype)initWithNibName:(NSString *)nibNameOrNil bundle:(NSBundle *)nibBundleOrNil{
    self = [super initWithNibName:nibNameOrNil bundle:nibBundleOrNil];
    if (self) {
        self.title = NSStringFromClass([self class]);
    }
    return self;
}
- (void)viewDidLoad {
    [super viewDidLoad];

#define Random arc4random()%256/255.0
    
    self.view.backgroundColor = [UIColor colorWithRed:Random green:Random blue:Random alpha:0.9f];
    
    UILabel *label = [[UILabel alloc]initWithFrame:CGRectMake(100, 100, 200, 100)];
    
    NSString *name = NSStringFromClass([self class]);
    label.text = name;
    
    [self.view addSubview:label];
}
@end

#import "ViewController4.h"
#import "ViewController4_1.h"
@interface ViewController4 ()

@end

@implementation ViewController4

- (void)viewDidLoad {
    [super viewDidLoad];
    
    UIButton *button = [UIButton buttonWithType:UIButtonTypeCustom];
    button.frame = CGRectMake(100, 100, 100, 100);
    button.backgroundColor = [UIColor lightGrayColor];
    [button addTarget:self action:@selector(onClick) forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button];
}
-(void)onClick{
    ViewController4_1 *vc = [[ViewController4_1 alloc]init];
    [self.navigationController pushViewController:vc animated:YES];
    
    NSLog(@"%f",self.tabBarController.tabBar.frame.size.height);
}
- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}



@end



```

