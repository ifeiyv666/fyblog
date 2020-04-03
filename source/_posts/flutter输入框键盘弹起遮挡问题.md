---
title: flutter输入框键盘弹起被遮挡问题
categories:
  - Flutter
tags:
  - 键盘遮挡
  - Flutter
  - TextField
abbrlink: 10105
date: 2020-04-3 11:32:06
---



#### 解决键盘弹起遮挡问题

   - Scaffold的resizeToAvoidBottomPadding属性（v1.1.9之后已废弃）
   - resizeToAvoidBottomInset：为true键盘弹起输入框会自动上移，为false不移动，如果输入框靠下，有可能被遮挡住。默认为true


```dart
  /// This flag is deprecated, please use [resizeToAvoidBottomInset]
  /// instead.
  ///
  /// Originally the name referred [MediaQueryData.padding]. Now it refers
  /// [MediaQueryData.viewInsets], so using [resizeToAvoidBottomInset]
  /// should be clearer to readers.
  @Deprecated(
    'Use resizeToAvoidBottomInset to specify if the body should resize when the keyboard appears. '
    'This feature was deprecated after v1.1.9.'
  )
  final bool resizeToAvoidBottomPadding;

  /// If true the [body] and the scaffold's floating widgets should size
  /// themselves to avoid the onscreen keyboard whose height is defined by the
  /// ambient [MediaQuery]'s [MediaQueryData.viewInsets] `bottom` property.
  ///
  /// For example, if there is an onscreen keyboard displayed above the
  /// scaffold, the body can be resized to avoid overlapping the keyboard, which
  /// prevents widgets inside the body from being obscured by the keyboard.
  ///
  /// Defaults to true.
  final bool resizeToAvoidBottomInset;
```

- 如果以上配置报错（键盘弹起，布局溢出）界面布局可以用滚动容器承载。eg:把当前界面放到SingleChildScrollView上
