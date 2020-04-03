---
title: Flutter开发之Scaffold Widget
categories:
  - Flutter
tags:
  - Flutter Scaffold
abbrlink: 10014
date: 2019-08-20 09:51:53
---




### Scaffold 

> 实现基本材料设计视觉布局结构


#### 构造函数(Constructors)


```dart
    Scaffold({
        Key key, 
        PreferredSizeWidget appBar, 
        Widget body,
        Widget floatingActionButton, 
        FloatingActionButtonLocation floatingActionButtonLocation, FloatingActionButtonAnimator floatingActionButtonAnimator, 
        List<Widget> persistentFooterButtons, 
        Widget drawer, 
        Widget endDrawer, 
        Widget bottomNavigationBar, 
        Widget bottomSheet, 
        Color backgroundColor, 
        bool resizeToAvoidBottomPadding, 
        bool resizeToAvoidBottomInset, 
        bool primary: true, 
        DragStartBehavior drawerDragStartBehavior: DragStartBehavior.start,
        bool extendBody: false 
    })
```



#### 属性（Properties）

- appBar → PreferredSizeWidget
  
> 顶部导航栏
  
- backgroundColor → Color
  
> 背景色
  
- body → Widget
  
> Scaffold的主要内容
  
- bottomNavigationBar → Widget
  
> 底部导航栏
  
- bottomSheet → Widget
  
>The persistent bottom sheet to display. [...]
  
- drawer → Widget
  
>显示在容器侧面的面板，通常隐藏在移动设备上。从左到右（TextDirection.ltr）或从右到左（TextDirection.rtl）滑入
  
- drawerDragStartBehavior → DragStartBehavior
  
>确定处理拖动开始行为的方式
  
- endDrawer → Widget
  
>显示在身体侧面的面板，通常隐藏在移动设备上。从右到左（TextDirection.ltr）或从左到右（TextDirection.rtl）滑动
  
- extendBody → bool
  
>如果为true，并且指定了bottomNavigationBar或persistentFooterButtons，则body将延伸到Scaffold的底部，而不是仅延伸到bottomNavigationBar或persistentFooterButtons的顶部
  
- floatingActionButton → Widget
  
>显示在容器上方的按钮，位于右下角
  
- floatingActionButtonAnimator → FloatingActionButtonAnimator
  
>Animator将floatingActionButton移动到新的floatingActionButtonLocation
  
- floatingActionButtonLocation → FloatingActionButtonLocation
  
>负责确定floatingActionButton的去向
  
- persistentFooterButtons → List<Widget>
  
> 一组显示在脚手架底部的按钮
  
- primary → bool
  
>此脚手架是否显示在屏幕顶部
  
- resizeToAvoidBottomInset → bool
  
>如果为true，则body和scaffold的浮动小部件应自行调整大小，以避免屏幕键盘的高度由环境MediaQuery的MediaQueryData.viewInsets底部属性定义
  
- resizeToAvoidBottomPadding → bool
  >不推荐使用此标志，请改用resizeToAvoidBottomInset,
@Deprecated（'使用resizeToAvoidBottomInset指定键盘出现时是否应调整主体大小'）

