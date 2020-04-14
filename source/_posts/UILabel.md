---
title: UILabel(Objc)
categories:
  - Objective-C
abbrlink: 10134
tags:
  - UILabel
date: 2017-03-03 18:53:19
---

#### UILabel

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
    
    //初始化window，并设置fram
    self.window = [[UIWindow alloc] initWithFrame:[UIScreen mainScreen].bounds];
    //[UIScreen mainScreen].bounds] 获取当前屏幕的大小
    
    //设置背景颜色
    [self.window setBackgroundColor:[UIColor purpleColor]];
    
    //Xcode 7.0 之后，必须有rootViewController
    //Xcode 7.0 之前，可以不设置rootViewController
    RootViewController * rootVC = [[RootViewController alloc]init];
    self.window.rootViewController = rootVC;
    //设置window为 keyWindow 并显示
    [self.window makeKeyAndVisible];
    

    return YES;
}
@implementation RootViewController
//视图已经加载
- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.
    //[self createUILabel];
    //[self  createNewLabel];
  //UILabel * label =(UILabel *)[self.view viewWithTag:9];
   // label.text = @"123";
    
}

-(void)createUILabel{
    
    //红50绿100蓝30
    //alpha 透明度，默认是1.0，取值范围0~1.0
    //利用RGB生成一个颜色
    //UIColor *color = [UIColor colorWithRed:50/255.0 green:100/255.0 blue:30/255.0 alpha:0.8];
    
    //设置self.view的背景色
    self.view.backgroundColor = [UIColor whiteColor];
    //CGRect rect = CGRectMake(50, 50, 100, 100);
    
    //初始化UILbel 并设置fram
    //重新设置fram，会把之前设置的fram覆盖
    UILabel * label = [[UILabel alloc] initWithFrame:CGRectMake(100, 100, 200, 200)];
    
    //设置label的背景色
    label.backgroundColor = [UIColor lightGrayColor];
    label.text = @"NSLineBreakByTruncatingTail,	    NSLineBreakByTruncatingMiddleNSLineBreakByTruncatingTail,NSLineBreakByTruncating ,MiddleNSLineBreakByTruncatingTail.NSLineBreakByTruncatingMiddleNSLineBreakByTruncatingTail,NSLineBreakByTruncatingMiddle";
    
    //设置字体的类型和大小
    label.font = [UIFont systemFontOfSize:20];
    
    //设置粗体
    label.font = [UIFont boldSystemFontOfSize:20];
    
    //设置斜体（不支持中文）
    label.font = [UIFont italicSystemFontOfSize:20];
    
    //获取所有字体
    NSLog(@"%@",[UIFont familyNames]);
   
    //设置字体，大小
    label.font = [UIFont fontWithName:@"Thonburi" size:20];
    
    //自适应宽度
    //label.adjustsFontSizeToFitWidth = YES;
    //内容对其方式
    label.textAlignment = NSTextAlignmentLeft;
    
    //label.textAlignment = NSTextAlignmentRight;
    //label.textAlignment = NSTextAlignmentCenter;
    
    //限制设置行数，如果文字不够，能显示多少行就显示多少行。
    //如果行高不够，能显示多少行就显示多少行。
    //默认值是0，表示行数最大
    label.numberOfLines = 0;
    
    label.lineBreakMode = NSLineBreakByTruncatingMiddle;
//    NSLineBreakByWordWrapping = 0,  根据单词截断
//    NSLineBreakByCharWrapping,      根据字符截断
//    NSLineBreakByClipping,          简单截断
//    NSLineBreakByTruncatingHead,    省略号在前
//    NSLineBreakByTruncatingTail,    省略号在后
//    NSLineBreakByTruncatingMiddle   省略号在中
    
    label.shadowColor = [UIColor blueColor];
    label.shadowOffset = CGSizeMake(3, 3);
    //设置透明度
    label.alpha = 0.8;
    //标识
    label.tag = 10;
    
    [self.view addSubview:label];
    
}


```

