---
title: UIScrollView(Objc)
categories:
  - Objective-C
abbrlink: 10135
tags:
  - UIScrollView
date: 2017-03-09 18:45:26
---

#### UIScrollView

```objc

#import "ViewController.h"

@interface ViewController ()<UIScrollViewDelegate>//遵守协议

{
//    滚动视图
    UIScrollView *_scrollView;
    
}

@property (weak, nonatomic) IBOutlet UIButton *myButton;
@end

@implementation ViewController

- (IBAction)onClick:(UIButton *)sender {
    [_scrollView setContentOffset:CGPointMake(0, 0) animated:YES];
}

- (void)viewDidLoad {
    [super viewDidLoad];
    
    [self createScrollView];
    [self addSubView];
    [self customScrollView];
    
    [self.view bringSubviewToFront:self.myButton];
    
    /*
//    [self.myButton  addTarget:self action:@selector(onClick) forControlEvents:UIControlEventTouchUpInside];
    
    //-(void)onClick{
    //    NSLog(@"onClick");
    //}
     */
    
 
}


//创建ScrollView
-(void)createScrollView{
//    初始化UIScrollView
    _scrollView = [[UIScrollView alloc]initWithFrame:self.view.bounds];
    
//    _scrollView = [[UIScrollView alloc]initWithFrame:CGRectMake(100, 100, 200, 200)];
//    设置背景色
    _scrollView.backgroundColor = [UIColor orangeColor];
//    设置代理
    _scrollView.delegate = self;
    
    [self.view addSubview:_scrollView];
    
}
-(void)addSubView{
//    获取文件路径
    NSString *path = [[NSBundle mainBundle]pathForResource:@"海贼02" ofType:@"jpg"];
//    转换成NSData
    NSData *data = [NSData dataWithContentsOfFile:path];
//    初始化图片
    UIImage *image = [UIImage imageWithData:data];
//    图片初始化后，会直接获得图片的width 和 height
//    NSLog(@"width = %lf---height = %lf",image.size.width,image.size.height);

//     初始化UIImageView
    UIImageView *imageView = [[UIImageView alloc]initWithFrame:CGRectMake(0, 0, image.size.width, image.size.height)];
    imageView.image = image;
    
//    设置滚动范围
//    必须给出滚动范围，这样滚动视图才能知道滚动的范围
    _scrollView.contentSize = CGSizeMake(image.size.width, image.size.height);
    
    
    [_scrollView addSubview:imageView];
}
// 定制ScrollView
-(void)customScrollView{
    
//    设置偏移量
//    [_scrollView setContentOffset:CGPointMake(200, 200)];

//    设置距离边框的距离
//    [_scrollView setContentInset:UIEdgeInsetsMake(100, 100, 100, 100)];
    
#pragma mark 滚动相关
    
//    设置是否可以超出边界
//    默认是YES，超出边界后，有回弹效果
//    设置NO，没有回弹效果
    _scrollView.bounces = YES;
    
//    在这里，想测试下面两个属性时，使用《海贼03.jpg》
//    当contentSize的宽度小于scrollView的宽度时，仍允许左右拖动，默认是NO
    _scrollView.alwaysBounceHorizontal = YES;
//    当contentSize的高度小于scrollView的高度时，仍允许上下手动，默认是NO
    _scrollView.alwaysBounceVertical = YES;
    
//    设置是否按页滚动，即每次滚动一个scrollView的宽度或高度，默认是NO
//    _scrollView.pagingEnabled = YES;
    
//    设置是否允许滚动，默认是YES
    _scrollView.scrollEnabled = YES;
    
//    设置是否显示滚动指示，默认是YES
    _scrollView.showsHorizontalScrollIndicator = YES;
    _scrollView.showsVerticalScrollIndicator = YES;
    
//    设置滚动指示的样式
    _scrollView.indicatorStyle = UIScrollViewIndicatorStyleWhite;
//    UIScrollViewIndicatorStyleDefault,
//    UIScrollViewIndicatorStyleBlack,
//    UIScrollViewIndicatorStyleWhite
    
//    设置滚动条距离scrollView边框的距离
    _scrollView.scrollIndicatorInsets = UIEdgeInsetsMake(0, 0, 30, 60);
    
    _scrollView.scrollsToTop = YES;
    
}
#pragma mark scrollView delegate
//将要拖拽
//当开始滚动视图时，会执行该方法
//一次有效的滑动执行一次（开始滑动到手指松开），
-(void)scrollViewWillBeginDragging:(UIScrollView *)scrollView{
    NSLog(@"将要拖拽");
}
//scrollView滚动时，就会调用该方法
//任何offset值的改变都会调用该方法。在滚动过程中，会调用多次
-(void)scrollViewDidScroll:(UIScrollView *)scrollView{
 //   CGPoint point = scrollView.contentOffset;
//    NSLog(@"偏移量%lf",point.x);
}
-(void)scrollViewWillEndDragging:(UIScrollView *)scrollView withVelocity:(CGPoint)velocity targetContentOffset:(inout CGPoint *)targetContentOffset{
    NSLog(@"将要结束拖拽");
}
//当手指离开屏幕的一瞬间，调用该方法，一次有效的滑动，只执行一次
-(void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate{
//    NSLog(@"%lf",scrollView.contentOffset.x);
    NSLog(@"拖拽结束");
//    [scrollView setContentOffset:CGPointMake(0, 0) animated:YES];
}

//将要减速
//该方法在scrollViewDidEndDragging 结束后执行
-(void)scrollViewWillBeginDecelerating:(UIScrollView *)scrollView{
    NSLog(@"将要减速");
}

-(void)scrollViewDidEndDecelerating:(UIScrollView *)scrollView{
    NSLog(@"减速结束");
    
//    [scrollView setContentOffset:CGPointMake(0, 0) animated:YES];
}
@end


```





```objc
#pragma mark 缩放 delegate
//当将要开始缩放时，执行该方法。一次有效的缩放，执行一次
-(void)scrollViewWillBeginZooming:(UIScrollView *)scrollView withView:(UIView *)view{
    NSLog(@"将要开始缩放");
}
//正在缩放
-(void)scrollViewDidZoom:(UIScrollView *)scrollView{
    NSLog(@"正在缩放");
    CGFloat value =  scrollView.zoomScale;
    NSLog(@"%f",value);
}
//结束缩放
-(void)scrollViewDidEndZooming:(UIScrollView *)scrollView withView:(UIView *)view atScale:(CGFloat)scale{
    NSLog(@"结束缩放");
}

//返回要缩放的UIView对象
-(UIView*)viewForZoomingInScrollView:(UIScrollView *)scrollView{
//  不允许返回scrollView
//  只能返回scrollView的子视图
    return scrollView.subviews[0];
}

//当用户点击状态栏后，滚动视图是否能够滚动到顶部
-(BOOL)scrollViewShouldScrollToTop:(UIScrollView *)scrollView{
//    当设置scrollToTop 为YES时，这里设置YES才会生效
    return NO;
}
//当滚动视图滚动到最顶端的时候，会执行该方法
-(void)scrollViewDidScrollToTop:(UIScrollView *)scrollView{
    NSLog(@"%s",__func__);
}

```

