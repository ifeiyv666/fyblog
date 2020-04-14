---
title: OC画图
categories:
  - Objective-C
abbrlink: 10118
tags:
  - OC画图
date: 2017-01-27 20:54:31
---

#### OC画图
```objc
#import "Customview.h"

@implementation Customview
{
    NSMutableArray *lineArray;
}

- (id)initWithFrame:(CGRect)frame
{
    self = [super initWithFrame:frame];
    if (self) {
        [self setBackgroundColor:[UIColor whiteColor]];
        
        UIButton *button=[UIButton buttonWithType:UIButtonTypeRoundedRect];
        [button setTitle:@"撤销" forState:UIControlStateNormal];
        [button addTarget:self action:@selector(doButton:) forControlEvents:UIControlEventTouchDown];
        button.frame=CGRectMake(110, 380, 100, 40);
        [button setBackgroundColor:[UIColor redColor]];
        [self addSubview:button];
        
        UIButton *button2=[UIButton buttonWithType:UIButtonTypeRoundedRect];
        [button2 setTitle:@"橡皮擦" forState:UIControlStateNormal];
        [button2 addTarget:self action:@selector(doButton:) forControlEvents:UIControlEventTouchDown];
        button2.frame=CGRectMake(110, 430, 100, 40);
        [button2 setBackgroundColor:[UIColor redColor]];
      
        [self addSubview:button2];

        //实例化数组（用来存放移动点的数组）
        lineArray =[[NSMutableArray alloc]init];
    }
    return self;
}

-(void)doButton:(id)button
{
    [lineArray removeLastObject];
    [self setNeedsDisplay];
}
-(void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event
{
    //创建触摸事件对象
    UITouch *touch = [touches anyObject];
    //拿到初始点
    CGPoint firstPoint = [touch locationInView:self];
    //转换成value对象
    NSValue *value = [NSValue valueWithCGPoint:firstPoint];
    //创建存放每个点的内层数组（一条线）
    NSMutableArray *pointArray = [[NSMutableArray alloc]init];
    [pointArray addObject:value];
    //把每一笔画对应 的数组放入外层数组
    [lineArray addObject:pointArray];
}
-(void)touchesMoved:(NSSet *)touches withEvent:(UIEvent *)event
{
    UITouch *touch = [touches anyObject];
      //拿到移动 时的每一个点
    CGPoint currentPoint = [touch locationInView:self];
    //拿到最后笔画对应的数组
    NSMutableArray *pointAaary = [lineArray lastObject];
    NSValue *value = [NSValue valueWithCGPoint:currentPoint];
    //把移动 的每一个点放入对应的数组
    [pointAaary addObject:value];
    //让视图重绘（调用该方法后self的drawrect方法会被调用）
    [self setNeedsDisplay];

}
-(void)touchesEnded:(NSSet *)touches withEvent:(UIEvent *)event
{
    
}
//iOS的绘图操作是在UIView类的drawRect方法中完成的，所以如果我们要想在一个UIView中绘图，需要写一个扩展UIView 的类，并重写drawRect方法，在这里进行绘图操作，程序会自动调用此方法进行绘图。
- (void)drawRect:(CGRect)rect
{
    //拿到当前绘图上下文环境
    CGContextRef currentText = UIGraphicsGetCurrentContext();
    //设置画笔线条的宽度
    CGContextSetLineWidth(currentText, 2);
    //将画笔设置为红色
    CGColorRef cf = [UIColor redColor].CGColor;
    CGContextSetStrokeColorWithColor(currentText, cf);
    
    for (int i = 0; i < [lineArray count]; i++) {
        //拿到每一个笔画对应的数组
       NSMutableArray *pArray = [lineArray objectAtIndex:i];
        for (int j = 0; j < [pArray count]-1; j++) {
            
            NSValue *previousValue = [pArray objectAtIndex:j];
            NSValue *currentValue = [pArray objectAtIndex:j+1];
            
            CGPoint previousPoint = [previousValue CGPointValue];
            CGPoint currentValuePoint = [currentValue CGPointValue];
            //设置画笔的起点
            CGContextMoveToPoint(currentText, previousPoint.x, previousPoint.y);
            //设置两点确定一条直线的另一点
            CGContextAddLineToPoint(currentText, currentValuePoint.x, currentValuePoint.y);
        }
        //提交描绘的轨迹，这才是真正画线的地方
        CGContextStrokePath(currentText);
    }
    
    
}
@end
```

