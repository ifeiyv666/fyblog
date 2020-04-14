---
title: UIWebView(Objc)
categories:
  - Objective-C
abbrlink: 10143
tags:
  - UIWebView
date: 2017-04-07 16:28:37
---

#### UIWebView

```objc
#import "ViewController.h"

@interface ViewController ()<UIWebViewDelegate>

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
//    初始化
    UIWebView *webView = [[UIWebView alloc]initWithFrame:self.view.bounds];
//    设置背景色
    webView.backgroundColor = [UIColor redColor];
    
//    设置代理
    webView.delegate = self;
    
    
//    添加到视图
    [self.view addSubview:webView];
    
//    网址
    NSString *path = @"http://www.baidu.com";
//    封装url,统一资源定位符，将字符串封装成可以识别的网址
    NSURL *url = [NSURL URLWithString:path];
//  请求类
    NSURLRequest *request = [NSURLRequest requestWithURL:url];
//  加载请求
    [webView loadRequest:request];
}

#pragma mark - delegate
//即将加载
-(BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType{
//  YES:加载网页信息
//  NO:不回网页信息
    NSLog(@"即将加载");
    return YES;
}
//已经开始加载
-(void)webViewDidStartLoad:(UIWebView *)webView{
    NSLog(@"已经开始加载");
}
//加载成功
-(void)webViewDidFinishLoad:(UIWebView *)webView{
    NSLog(@"加载成功");
}
-(void)webView:(UIWebView *)webView didFailLoadWithError:(NSError *)error{
    NSLog(@"加载失败");
}
@end

```

```objc

#import "ViewController.h"

@interface ViewController ()<UITableViewDataSource,UITableViewDelegate>
{
    UITableView *_tableView;
}
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    [self createUITableView];
}
-(void)createUITableView{
//    初始化并设置样式和frame
    _tableView = [[UITableView alloc]initWithFrame:self.view.bounds style:UITableViewStylePlain];
//    设置背景色
    _tableView.backgroundColor = [UIColor orangeColor];
    
//    设置代理
    _tableView.dataSource = self;
    _tableView.delegate = self;
    
    [self.view addSubview:_tableView];
    
//    设置tableView的头视图
    UIImageView *headerImageView = [[UIImageView alloc]initWithFrame:CGRectMake(0, 0, self.view.frame.size.width, 200)];
    headerImageView.image = [UIImage imageNamed:@"1.jpg"];
    _tableView.tableHeaderView = headerImageView;
//    设置tableView的脚视图
    UIImageView *footerImageView = [[UIImageView alloc]initWithFrame:CGRectMake(0, 0, self.view.frame.size.width, 200)];
    footerImageView.image = [UIImage imageNamed:@"2.jpg"];
    _tableView.tableFooterView = footerImageView;
}
#pragma mark - 
#pragma mark dataSource
//返回多少个分组
-(NSInteger)numberOfSectionsInTableView:(UITableView *)tableView{
    return 2;
}
//返回每组有几行
-(NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section{
    if (section == 0) {
        return 10;
    }
    return 15;
}
-(UITableViewCell*)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath{
    
//    1.标识
    static NSString *identifier = @"cellID";
    
//    2.从tableView复用池中取cell
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:identifier];
//    3.如果从复用池中取不到cell,就创建新的
    if (cell == nil) {
        cell = [[UITableViewCell alloc]initWithStyle:UITableViewCellStyleDefault reuseIdentifier:identifier];
    }
    
    cell.textLabel.text = [NSString stringWithFormat:@"第%ld组-第%ld行",indexPath.section,indexPath.row];
    
    return cell;
}
#pragma mark -
#pragma mark delegate
////设置头标题
-(NSString*)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section{
    if (section == 0) {
        return @"第一组头标题";
    }
    return @"第二组头标题";
}
//设置头标题高度
-(CGFloat)tableView:(UITableView *)tableView heightForHeaderInSection:(NSInteger)section{
//    默认22
    return 40;
}
//设置分组脚标题
-(NSString*)tableView:(UITableView *)tableView titleForFooterInSection:(NSInteger)section{
    if (section == 0) {
        return @"第一组脚标题";
    }
    return @"第二组脚标题";
}
//设置脚标题的高度
-(CGFloat)tableView:(UITableView *)tableView heightForFooterInSection:(NSInteger)section{
    return 40;
}
//返回自定义分组的头标和脚标，会把前面设置的标题覆盖
//必须设置头标题或头标题高度，否则本方法不生效
-(UIView*)tableView:(UITableView *)tableView viewForHeaderInSection:(NSInteger)section{
    UIButton *button = [UIButton buttonWithType:UIButtonTypeCustom];
    button.frame = CGRectMake(0, 0, self.view.frame.size.width, 40);
    [button setTitle:@"分组标题" forState:UIControlStateNormal];
    button.backgroundColor = [UIColor purpleColor];
    [button addTarget:self action:@selector(onClick) forControlEvents:UIControlEventTouchUpInside];
    return button;
}
-(void)onClick{
    NSLog(@"点点点点点");
}
//必须设置脚标题或脚标题高度，否则本方法不生效
-(UIView*)tableView:(UITableView *)tableView viewForFooterInSection:(NSInteger)section{
    UIImageView *imageView = [[UIImageView alloc]initWithFrame:CGRectMake(0, 0, self.view.frame.size.width, 40)];
    imageView.image = [UIImage imageNamed:@"6.jpg"];
    return imageView;
}
@end

```

```objc
#import "ViewController.h"

@interface ViewController ()<UITableViewDelegate,UITableViewDataSource>
{
//    表格视图
    UITableView *_tableView;
}
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
 
    [self createUITableView];
//    [_tableView performSelector:@selector(reloadData) withObject:nil afterDelay:5];
}
//创建UITableView
-(void)createUITableView{
    
//    初始化UITableView
    _tableView = [[UITableView alloc]initWithFrame:self.view.bounds style:UITableViewStylePlain];
//    UITableViewStylePlain, 平铺样式
//    UITableViewStyleGrouped 分组样式
    
//    背景色
    _tableView.backgroundColor = [UIColor orangeColor];
    
//    设置数据源代理
    _tableView.dataSource = self;
//    设置代理
    _tableView.delegate = self;
    
    [self.view addSubview:_tableView];
}
#pragma mark -
#pragma mark dataSource
//返回多少个分组
-(NSInteger)numberOfSectionsInTableView:(UITableView *)tableView{
    NSLog(@"numberOfSectionsInTableView");
    return 2;
}
//每组有多少行
-(NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section{
    NSLog(@"numberOfRowsInSection");
    if (section == 0) {
        return 10;
    }
    return 20;
    
}
-(UITableViewCell*)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath{
//    NSLog(@"cellForRowAtIndexPath");
//    indexPath
//    表示当cell在表格视图中的位置
//    indexPath.section 代表的是cell所在的分组
//    indexPath.row     代表的是cell所在分组的行的位置
    
    
//    1.表格的标识
    static NSString *identifier = @"cellID";
    
//    2.按照标识从tableView复用池中取cell
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:identifier];
//    3.如果在复用池中找不以Cell,就创建新的Cell
    if (cell == nil) {
        cell = [[UITableViewCell alloc]initWithStyle:UITableViewCellStyleDefault reuseIdentifier:identifier];
//        UITableViewCellStyleDefault,
//        UITableViewCellStyleValue1,
//        UITableViewCellStyleValue2,
//        UITableViewCellStyleSubtitle
    }
//    设置展示标题
    cell.textLabel.text = [NSString stringWithFormat:@"第%ld组",indexPath.section];
//    设置展示详细标题
    cell.detailTextLabel.text = [NSString stringWithFormat:@"第%ld行",indexPath.row];
//    设置展示图片
    cell.imageView.image = [UIImage imageNamed:@"1"];
    
//    附件按钮类型
    cell.accessoryType = UITableViewCellAccessoryDetailButton;
    
//    UITableViewCellAccessoryNone, 无样式
//    UITableViewCellAccessoryDisclosureIndicator箭头
//UITableViewCellAccessoryDetailDisclosureButton 箭头+信息按钮
//    UITableViewCellAccessoryCheckmark,对勾
//    UITableViewCellAccessoryDetailButton 信息按钮
    
//=============================================
//    UIView *accessView = [[UIView alloc]initWithFrame:CGRectMake(0, 0, 40, 40)];
//    accessView.backgroundColor = [UIColor blackColor];
////    设置自定义的附件视图
//    cell.accessoryView = accessView;
//=============================================
    
    
//    选中样式
    cell.selectionStyle = UITableViewCellSelectionStyleDefault;
//    UITableViewCellSelectionStyleNone,
//    UITableViewCellSelectionStyleBlue,
//    UITableViewCellSelectionStyleGray,
//    UITableViewCellSelectionStyleDefault
    
//    设置选中背景View
    UIView *BackgroundView = [[UIView alloc]initWithFrame:CGRectMake(0, 0, 50, 50)];
    BackgroundView.backgroundColor = [UIColor clearColor];
    cell.selectedBackgroundView = BackgroundView;
    
//    UIImageView *imageView = [[UIImageView alloc]initWithFrame:CGRectMake(0, 0, self.view.frame.size.width, 44)];
//    imageView.image = [UIImage imageNamed:@"1"];
//    cell.selectedBackgroundView = imageView;
    
    return cell;
}

#pragma mark -
#pragma mark delegate
-(void)tableView:(UITableView *)tableView accessoryButtonTappedForRowWithIndexPath:(NSIndexPath *)indexPath{
    NSLog(@"点击了附件按钮");
}
//设置行高
-(CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath{
//    默认行高 44
    return 80;
}
//设置分组的头标题
-(NSString*)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section{
    if (section == 0) {
        return @"第一组组标题";
    }
    return @"第二组组标题";
}
//设置脚标题
-(NSString*)tableView:(UITableView *)tableView titleForFooterInSection:(NSInteger)section{
    if (section == 0) {
        return @"第一组脚标";
    }
    return @"第二组脚标";
}
//组头的高度
-(CGFloat)tableView:(UITableView *)tableView heightForHeaderInSection:(NSInteger)section{
//    默认高度是22
    return 40;
}
//组尾的高度
-(CGFloat)tableView:(UITableView *)tableView heightForFooterInSection:(NSInteger)section{
//    默认高度是22
    return 40;
}
@end


```



```objc
#import "ViewController.h"

@interface ViewController ()<UITableViewDataSource,UITableViewDelegate>
{
    UITableView *_tableView;
    NSMutableArray *_dataArray;
}
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    [self createUITableView];
    [self createDataArray];
    
    self.navigationItem.rightBarButtonItem = self.editButtonItem;
}
//编辑按钮触发的方法
-(void)setEditing:(BOOL)editing animated:(BOOL)animated{
    NSLog(@"%d",editing);
//    重新调用父类的方法，处于Done字样时，editing=YES,处于Edit样式时，editing = NO.
    [super setEditing:editing animated:YES];
    
//    设置tableView的可编辑性
    [_tableView setEditing:editing animated:YES];
}
-(void)createUITableView{
//    初始化UITableView 设置样式和frame
    _tableView = [[UITableView alloc]initWithFrame:self.view.bounds style:UITableViewStylePlain];
//    设置背景色
    _tableView.backgroundColor = [UIColor orangeColor];
//    设置代理
    _tableView.dataSource = self;
    _tableView.delegate = self;
//    添加到视图
    [self.view addSubview:_tableView];
}
-(void)createDataArray{
    
    _dataArray = [NSMutableArray array];
    
//    数据源中要添加两组数据：删除的、增加的
    NSMutableArray *deleteArray = [NSMutableArray array];
    for (int i = 0 ; i < 10;  i ++) {
        NSString *deleteStr = [NSString stringWithFormat:@"被删除的第%d行",i];
        [deleteArray addObject:deleteStr];
    }
    NSMutableArray *insertArray = [NSMutableArray array];
    for (int i = 0 ; i < 10; i ++) {
        NSString *insertStr = [NSString stringWithFormat:@"增加的第%d行",i];
        [insertArray addObject:insertStr];
    }
    
    [_dataArray addObject:deleteArray];
    [_dataArray addObject:insertArray];
    NSLog(@"%@",_dataArray);
}
#pragma mark -
#pragma mark dataSource
//返回有多少组
-(NSInteger)numberOfSectionsInTableView:(UITableView *)tableView{
    return _dataArray.count;
}
//每组有多少行
-(NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section{
    
    NSMutableArray *array = [_dataArray objectAtIndex:section];
    
    return array.count;
}
-(UITableViewCell*)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath{
//    1.定义标识
    static NSString *identifier = @"cellID";
//    2.从tableView复用池中取cell
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:identifier];
//    3.如果取不到cell,就创建新的cell
    if (cell == nil) {
        cell = [[UITableViewCell alloc]initWithStyle:UITableViewCellStyleDefault reuseIdentifier:identifier];
    }
    
//    cell.textLabel.text = _dataArray[indexPath.section][indexPath.row];
    
//    赋值
    cell.textLabel.text = [[_dataArray objectAtIndex:indexPath.section]objectAtIndex:indexPath.row];
    
    return cell;
}
#pragma mark -
#pragma mark delegate
//选中了哪一行
-(void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath{
//    NSLog(@"选中了哪一行");
    NSLog(@"第%ld组-第%ld行",indexPath.section,indexPath.row);
}
//反选
-(void)tableView:(UITableView *)tableView didDeselectRowAtIndexPath:(NSIndexPath *)indexPath{
//    NSLog(@"didDeselectRowAtIndexPath");
    NSLog(@"----第%ld组-第%ld行",indexPath.section,indexPath.row);
}
//设置tableView 的编辑状态
-(UITableViewCellEditingStyle)tableView:(UITableView *)tableView editingStyleForRowAtIndexPath:(NSIndexPath *)indexPath{
    
//    UITableViewCellEditingStyleNone,无效果
//    UITableViewCellEditingStyleDelete,删除
//    UITableViewCellEditingStyleInsert 增加
    
    if (indexPath.section == 0) {
        return UITableViewCellEditingStyleDelete;
    }else{
        return UITableViewCellEditingStyleInsert;
    }
}
-(void)tableView:(UITableView *)tableView commitEditingStyle:(UITableViewCellEditingStyle)editingStyle forRowAtIndexPath:(NSIndexPath *)indexPath{
    
    if (editingStyle == UITableViewCellEditingStyleDelete) {
//        删除当前对应行的数据源
        [[_dataArray objectAtIndex:indexPath.section]removeObjectAtIndex:indexPath.row];
        
//        [tableView reloadData];
//       刷新表
        [tableView deleteRowsAtIndexPaths:@[indexPath] withRowAnimation:UITableViewRowAnimationNone];
    }else{
        NSString *insertStr = @"我是新来的";
//        数据源添加新数据
        [[_dataArray objectAtIndex:indexPath.section] insertObject:insertStr atIndex:indexPath.row];
//        刷表
//        [tableView reloadData];
        [tableView insertRowsAtIndexPaths:@[indexPath] withRowAnimation:UITableViewRowAnimationNone];
    }
}
//是否允许某一行被编辑
-(BOOL)tableView:(UITableView *)tableView canEditRowAtIndexPath:(NSIndexPath *)indexPath{
//    if (indexPath.row % 2 == 0) {
//        return  YES;
//    }
//    return NO;
    return YES;
}
//移动要实现的方法
-(void)tableView:(UITableView *)tableView moveRowAtIndexPath:(NSIndexPath *)sourceIndexPath toIndexPath:(NSIndexPath *)destinationIndexPath{
//    sourceIndexPath 将要移动的cell的位置信息
//    destinationIndexPath 目的位置信息
    
//    根据sourceIndexPath.section来获得第section组的数据
    NSMutableArray *sourceArray = _dataArray[sourceIndexPath.section];
//    取出要移动cell所在行的数据
    NSString *sourceStr = sourceArray[sourceIndexPath.row];
//    删除要移动cell所在行的数据
    [sourceArray removeObjectAtIndex:sourceIndexPath.row];
    
//    根据destinationIndexPath.section来获取要插入的数组
    NSMutableArray *destinationArray = _dataArray[destinationIndexPath.section];
    
    [destinationArray insertObject:sourceStr atIndex:destinationIndexPath.row];
}
//能否移动
-(BOOL)tableView:(UITableView *)tableView canMoveRowAtIndexPath:(NSIndexPath *)indexPath{
    if (indexPath.section == 0) {
        return NO;
    }
    return YES;
}
@end




```

