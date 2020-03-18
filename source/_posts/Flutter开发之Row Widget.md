---
title: Flutter开发之Row Widget
categories:
  - Flutter
tags:
  - Flutter Row
abbrlink: 10013
date: 2019-08-18 17:43:24
---



### Row

> 一个在水平数组中显示它的子级的小部件

要使子级扩展以填充可用的水平空间, 请将子级包裹在一个展开的小部件中。

*想使用竖直布局的，请前往->[ Column]()*

如果你只有一个子级, 那就考虑用 "对齐" 或 "中心" 来定位子级。

>本示例将可用空间划分为三个 (水平), 并将文本置于前两个单元格中的中心, 并将 Flutter 图标置于第三个单元格的中心: 
```
Row(
  children: <Widget>[
    Expanded(
      child: Text('Deliver features faster', textAlign: TextAlign.center),
    ),
    Expanded(
      child: Text('Craft beautiful UIs', textAlign: TextAlign.center),
    ),
    Expanded(
      child: FittedBox(
        fit: BoxFit.contain, // otherwise the logo will be tiny
        child: const FlutterLogo(),
      ),
    ),
  ],
)

```
**效果图：**<br>
![Row]("")



