---
title: Flutter开发之RaisedButton Widget
categories:
  - Flutter
tags:
  - Flutter RaisedButton
abbrlink: 10012
date: 2019-08-17 22:15:14
---



### RaisedButton
   >一个凸起的按钮
   
   
如果`onPressed`（即为按钮点击事件）回调为`null`，则该按钮将被禁用，默认情况下将类似于`disabledColor`中的平面按钮。如果您尝试更改按钮的颜色并且没有任何效果，请检查您是否正在传递非`null` `onPressed`处理程序。


如果您想为点击提供墨水飞溅效果,但不想使用按钮,请考虑直接使用[inkwell](https://api.flutter.dev/flutter/material/InkWell-class.html)。

凸起按钮的最小尺寸为88.0×36.0，可以用`ButtonTheme`覆盖。

**此示例演示如何呈现禁用的RaisedButton，启用的RaisedButton以及最后一个具有渐变背景的RaisedButton:**

![Img](https://flutter.github.io/assets-for-api-docs/assets/material/raised_button.png)

源码：
```
Widget build(BuildContext context) {
  return Center(
    child: Column(
      mainAxisSize: MainAxisSize.min,
      children: <Widget>[
        const RaisedButton(
          onPressed: null,
          child: Text(
            'Disabled Button',
            style: TextStyle(fontSize: 20)
          ),
        ),
        const SizedBox(height: 30),
        RaisedButton(
          onPressed: () {},
          child: const Text(
            'Enabled Button',
            style: TextStyle(fontSize: 20)
          ),
        ),
        const SizedBox(height: 30),
        RaisedButton(
          onPressed: () {},
          textColor: Colors.white,
          padding: const EdgeInsets.all(0.0),
          child: Container(
            decoration: const BoxDecoration(
              gradient: LinearGradient(
                colors: <Color>[
                  Color(0xFF0D47A1),
                  Color(0xFF1976D2),
                  Color(0xFF42A5F5),
                ],
              ),
            ),
            padding: const EdgeInsets.all(10.0),
            child: const Text(
              'Gradient Button',
              style: TextStyle(fontSize: 20)
            ),
          ),
        ),
      ],
    ),
  );
}
```

#### 构造函数（Constructors）


> 创建一个填充按钮

```
   RaisedButton({
      Key key, 
      @required VoidCallback onPressed,
      ValueChanged<bool> onHighlightChanged,
      ButtonTextTheme textTheme, 
      Color textColor, 
      Color disabledTextColor, 
      Color color, 
      Color disabledColor, 
      Color highlightColor, 
      Color splashColor, 
      Brightness colorBrightness, 
      double elevation, 
      double highlightElevation, 
      double disabledElevation, 
      EdgeInsetsGeometry padding, 
      ShapeBorder shape, 
      Clip clipBehavior: Clip.none, MaterialTapTargetSize materialTapTargetSize, Duration animationDuration, 
      Widget child 
   })
```

> 从一对小部件创建一个填充按钮，用作按钮的图标和标签

```
   RaisedButton.icon({
      Key key, 
      @required VoidCallback onPressed,
      ValueChanged<bool> onHighlightChanged,
      ButtonTextTheme textTheme, 
      Color textColor, 
      Color disabledTextColor, 
      Color color, 
      Color disabledColor, 
      Color highlightColor, 
      Color splashColor, 
      Brightness colorBrightness, 
      double elevation, 
      double highlightElevation, 
      double disabledElevation, 
      ShapeBorder shape, 
      Clip clipBehavior, 
      MaterialTapTargetSize materialTapTargetSize,
      Duration animationDuration, 
      @required Widget icon, 
      @required Widget label 
   })
```


#### 属性（Properties）

- `animationDuration → Duration`
   > 动画的持续时间

- `child → Widget`
   > 按钮的标签部件

- `clipBehavior → Clip`
   > 根据此选项，内容将被剪裁（或不剪辑）

- `color → Color`
   > 按钮的填充颜色，由其材料显示，同时处于默认（未按下，已启用）状态

- `colorBrightness → Brightness`
   > 用于设置按钮的主题亮度

- `disabledColor → Color`
   > 禁用按钮时按钮的填充颜色

- `disabledElevation → double`
   > 按钮相对于其父级的高度

- `disabledTextColor → Color`
   > 禁用按钮时用于此按钮文本的颜色

- `elevation → double`
   > 放置此按钮相对于其父按钮的Z坐标

- `enabled → bool`
   > 设置启用还是禁用按钮

- `hashCode → int`
   > 此对象的哈希码(只读)

- `height → double`
   > 按钮的垂直范围(即高度)

- `highlightColor → Color`
   > 按钮的InkWell的高亮颜色

- `highlightElevation → double`
   > 启用并按下按钮时按钮相对于其父级的高度

- `key → Key`
   > 控制一个小部件如何替换树中的另一个小部件

- `materialTapTargetSize → MaterialTapTargetSize`
   > 配置点击目标的最小尺寸

- `minWidth → double`
   > 按钮占据的最小水平范围(最小宽度)

- `onHighlightChanged → ValueChanged<bool>`
   > 由底层InkWell小部件的`InkWell.onHighlightChanged`回调调用

- `onPressed → VoidCallback`
   > 点击或以其他方式激活按钮时调用的回调

- `padding → EdgeInsetsGeometry`
   > buttons子级的内部填充

- `runtimeType → Type`
   > 表示对象的运行时类型(只读)

- `shape → ShapeBorder`
   > 按钮的阴影效果设置

- `splashColor → Color`
   > 按钮墨水的泼溅颜色

- `textColor → Color`
   > 按钮的文本颜色

- `textTheme → ButtonTextTheme`
   > 定义按钮的基色，以及按钮的最小尺寸，内部填充和形状的默认值



