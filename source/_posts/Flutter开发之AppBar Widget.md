---
title: Flutter开发之AppBar Widget
categories:
  - Flutter
tags:
  - Flutter AppBar
abbrlink: 10008
date: 2019-08-13 14:12:33
---




### AppBar

应用栏通常用于Scaffold.appBar属性，该属性将应用栏放置在屏幕顶部的固定高度小部件中。对于可滚动的应用栏，请参阅[SliverAppBar](https://api.flutter.dev/flutter/material/SliverAppBar-class.html)，它将一个AppBar嵌入到一个条子中，以便在CustomScrollView中使用。

AppBar在底部（如果有）上方显示工具栏小部件，前导，标题和操作。底部通常用于TabBar。如果指定了flexibleSpace窗口小部件，则它将堆叠在工具栏和底部窗口小部件后面。下图显示了当编写语言从左到右（例如英语）时，每个插槽在工具栏中的显示位置：
![image](https://flutter.github.io/assets-for-api-docs/assets/material/app_bar.png)

如果省略了前导小部件，但AppBar位于带有抽屉的脚手架中，则会插入一个按钮以打开抽屉。否则，如果最近的导航器具有任何先前的路径，则会插入BackButton。可以通过将automatedImplyLeading设置为false来关闭此行为。在这种情况下，空的前导小部件将导致中间/标题小部件拉伸开始。


#### 构造方法（Constructors）

```dart
    AppBar({
        Key key, 
        Widget leading, 
        bool automaticallyImplyLeading: true, 
        Widget title, 
        List<Widget> actions, 
        Widget flexibleSpace, 
        PreferredSizeWidget bottom, 
        double elevation, 
        ShapeBorder shape, 
        Color backgroundColor, 
        Brightness brightness, 
        IconThemeData iconTheme, 
        IconThemeData actionsIconTheme, 
        TextTheme textTheme, 
        bool primary: true, 
        bool centerTitle, double titleSpacing: NavigationToolbar.kMiddleSpacing, 
        double toolbarOpacity: 1.0, 
        double bottomOpacity: 1.0 
    })
```
eg:
```dart
AppBar(
  title: Text('My Fancy Dress'),
  actions: <Widget>[
    IconButton(
      icon: Icon(Icons.playlist_play),
      tooltip: 'Air it',
      onPressed: _airDress,
    ),
    IconButton(
      icon: Icon(Icons.playlist_add),
      tooltip: 'Restitch it',
      onPressed: _restitchDress,
    ),
    IconButton(
      icon: Icon(Icons.playlist_add_check),
      tooltip: 'Repair it',
      onPressed: _repairDress,
    ),
  ],
)
```

#### 属性（Properties）

- actions → List<Widget>
  
>要在标题小部件后显示的小部件
  
- actionsIconTheme → IconThemeData
  
>用于应用栏操作中显示的图标的颜色，不透明度和大小。仅当操作的主题不同于应用栏的主要小部件中显示的图标时，才应使用此选项
  
- automaticallyImplyLeading → bool
  
>Controls whether we should try to imply the leading widget if null. [...]
  
- backgroundColor → Color
  
>用于应用栏材质的颜色。通常这应该与亮度，iconTheme，textTheme一起设置。
  
- bottom → PreferredSizeWidget
  
>此小组件显示在应用栏的底部
  
- bottomOpacity → double
  
>应用栏底部的不透明程度(0.0 - 1.0)
  
- brightness → Brightness
  
>应用栏材质的亮度。通常，这与backgroundColor，iconTheme，textTheme一起设置
  
- centerTitle → bool
  
>标题是否居中
  
- elevation → double
  
>放置此应用程序栏相对于其父应用程序栏的Z坐标
  
- flexibleSpace → Widget
  
>此小组件堆叠在工具栏和选项卡栏后面。它的高度与应用栏的整体高度相同
  
- iconTheme → IconThemeData
  
>用于应用栏图标的颜色，不透明度和大小。通常，这与backgroundColor，brightness，textTheme一起设置
  
- leading → Widget
  
>要在标题之前显示的小部件
  
- preferredSize → Size
  
>高度为kToolbarHeight和底部窗口小部件首选高度之和的大小
  
- primary → bool
  
>此应用栏是否显示在屏幕顶部
  
- shape → ShapeBorder
  
> 形状和阴影
  
- textTheme → TextTheme
  
>应用栏中用于文本的排版样式。通常，这与亮度backgroundColor，iconTheme一起设置
  
- title → Widget
  
> appbar中显示的主要小部件
  
- titleSpacing → double
  
> 横轴上标题内容周围的间距。即使没有前导内容或操作，也会应用此间距。如果希望title占用所有可用空间，请将此值设置为0.0
  
- toolbarOpacity → double
  
  >应用栏的工具栏部分透明度(0.0-1.0)

