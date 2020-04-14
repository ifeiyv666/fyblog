---
title: UISlider(Objc)
categories:
  - Objective-C
abbrlink: 10137
tags:
  - UISlider
date: 2017-03-25 15:21:56
---

#### UISlider

```objc

#import "ViewController.h"

@interface ViewController ()

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view, typically from a nib.
//    slider高度是固定的
    UISlider *slider = [[UISlider alloc]initWithFrame:CGRectMake(100, 100, 200, 30)];
    slider.tag = 10;
//    最小值
    slider.minimumValue = 0;
//    最大值
    slider.maximumValue = 255;
//    设置当前值
    slider.value = 200;
    
//    未滑动到的颜色
    slider.maximumTrackTintColor = [UIColor greenColor];
//    已经滑动过的颜色
    slider.minimumTrackTintColor = [UIColor orangeColor];
//    小球（滑块）颜色
    slider.thumbTintColor = [UIColor blackColor];
//    设置图片
//    最左端图片
    slider.minimumValueImage = [UIImage imageNamed:@"blackHeart"];
//   最右端图片
    slider.maximumValueImage = [UIImage imageNamed:@"redHeart"];
//    设置滑块正常状态下的图片
    [slider setThumbImage:[UIImage imageNamed:@"blackHeart"] forState:UIControlStateNormal];
//    设置滑块高亮状态下的图片
    [slider setThumbImage:[UIImage imageNamed:@"redHeart"] forState:UIControlStateHighlighted];
    
    [slider addTarget:self action:@selector(valueChange:) forControlEvents:UIControlEventValueChanged];
    [self.view addSubview:slider];
    
    UISlider *greenSlider = [[UISlider alloc]initWithFrame:CGRectMake(100, 200, 200, 80)];
    greenSlider.tag = 11;
    greenSlider.minimumValue = 0;
    greenSlider.maximumValue = 255;
    [greenSlider addTarget:self action:@selector(valueChange:) forControlEvents:UIControlEventValueChanged];
    
    [self.view addSubview:greenSlider];
    
    UISlider *blueSlider = [[UISlider alloc]initWithFrame:CGRectMake(100, 300, 200, 100)];
    blueSlider.tag = 12;
    blueSlider.minimumValue = 0;
    blueSlider.maximumValue = 255;
    [blueSlider addTarget:self action:@selector(valueChange:) forControlEvents:UIControlEventValueChanged];
    [self.view addSubview:blueSlider];
}
-(void)valueChange:(UISlider*)slider{
    NSLog(@"---%lf",slider.value);
    UISlider *redSlider = (UISlider *)[self.view viewWithTag:10];
    UISlider *greenSlider = (UISlider *)[self.view viewWithTag:11];
    UISlider *blueSlider = (UISlider *)[self.view viewWithTag:12];
    
    [self.view setBackgroundColor:[UIColor colorWithRed:redSlider.value/255.0 green:greenSlider.value/255.0 blue:blueSlider.value/255.0 alpha:1.0]];
    

}

@end


```


