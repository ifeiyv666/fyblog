---
title: Flutter 字符串多余n行折叠，点击展开
categories:
  - Flutter
tags:
  - Flutter 字符串
abbrlink: 10114
date: 2019-11-24 35:59:22
---


#### flutter 字符串多余n行折叠，点击展开

- 获取TextPainter

```dart
 TextPainter fetchTextPainter(String text, TextStyle style, int maxLine,
      double minWidth, double maxWidth) {
    return TextPainter(
        maxLines: maxLine,
        text: TextSpan(text: text, style: style),
        textDirection: TextDirection.ltr)
      ..layout(maxWidth: maxWidth, minWidth: minWidth);
  }
```

- 判断是否超过n行，需要截断文本

```dart
bool isExpansion(String text, TextStyle style, int maxLine, double minWidth,
      double maxWidth) {
    TextPainter _textPainter =
        fetchTextPainter(text, style, maxLine, minWidth, maxWidth);
    if (_textPainter.didExceedMaxLines) {
      //这里判断 文本是否截断
      return true;
    } else {
      return false;
    }
  }
```

- 超过n行，需要展开。展开箭头放在文本右下角，移除两个字符（根据需求）用来放展开箭头

```dart
  String expansionString(String text, TextStyle style, int maxLine,
      double minWidth, double maxWidth) {
    TextPainter _textPainter =
        fetchTextPainter(text, style, maxLine, minWidth, maxWidth);
    var end = _textPainter
        .getPositionForOffset(
            Offset(_textPainter.size.width, _textPainter.size.height))
        .offset;
    return text.substring(0, end - 2) + "...";
  }
```
