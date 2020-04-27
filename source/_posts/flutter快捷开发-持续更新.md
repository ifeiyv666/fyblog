---
title: flutter快捷开发-持续更新
categories:
  - Flutter
tags:
  - Flutter开发
abbrlink: 10015
date: 2020-04-24 10:38:15

---



#### 1. 封装Text,只向外提供常用的属性，根据需求适当需改

```dart
  static Widget text(String data, {
      double textScaleFactor = 1.0,
      Color color = Colors.black, 
      double fontSize = 16, 
      FontWeight fontWeight = FontWeight.normal, 
      FontStyle fontStyle = FontStyle.normal
      }){
    return Text(data,
    textScaleFactor: textScaleFactor,
    style: TextStyle(
        color: color,
        fontSize: fontSize,
        fontWeight: fontWeight, 
        fontStyle: fontStyle,
    ),);
  }

```



#### 2. 检测当前主题

```dart
  static bool isDark(BuildContext context){
    final Brightness brightnessValue = Theme.of(context).brightness;
    return brightnessValue == Brightness.dark;
  }
```



#### 3. 根据主题设置颜色

```dart
  //是否是深色模式 true dark主题模式  false light主题模式
  static bool isDark(context){
    return Theme.of(context).brightness == Brightness.dark;
  }
  static Color dyColor(BuildContext context,darkColor,lightColor) => isDark(context) ? darkColor : lightColor;
  //背景颜色
  static Color dyBgColor(BuildContext context) =>  isDark(context) ?  MColor.darkBgColor : Colors.white;
  //字体颜色
  static Color dyFontColor(BuildContext context) =>  isDark(context) ?  MColor.textColor : MColor.black;
  static Color dyRedColor(BuildContext context) =>  isDark(context) ?  Colors.red[400] : Colors.red;
  static Color dyBlueColor(BuildContext context) =>  isDark(context) ?  Colors.blue[600] : Colors.blue;

```



#### 4. 返回一个字体不跟随系统缩放的Widget

```dart
  static noScaleWidget(Widget widget){
    return MediaQuery(
            data: MediaQueryData
                  .fromWindow(WidgetsBinding.instance.window)
                  .copyWith(textScaleFactor: 1),
            child: widget);
  }
```



#### 5. 取随机颜色（需要`import 'dart:math';`）

```dart
 static Color getRandomColor() {
    var random = new Random();
    int r = random.nextInt(255);
    int g = random.nextInt(255);
    int b = random.nextInt(255);
    return Color.fromARGB(255, r, g, b);
  }
```



