---
title: Flutter Flutter.h file not found
categories:
  - Flutter
tags:
  - Flutter的坑
abbrlink: 10005
date: 2019-07-05 11:34:54
---



####  1. 'Flutter/Flutter.h' file not found

##### 解决方案1.

点击这里[前往下载](https://github.com/flutter/flutter/tree/master/packages/flutter_tools/templates/cocoapods)对应版本文件,替换原来的文件`ios/Podfile`内容，删除`ios/Podfile.lock`,重新 `pod install` 即可

##### 解决方案2.

执行代码：`flutter run -v` 和 `flutter doctor -v` 检测配置是否成功


可能会出现以下情况：

Mac os 10.15 无法打开“idevice_id”,因为无法验证开发者

Mac os 10.15 无法打开“ideviceinfo”,因为无法验证开发者

解决方法 打开终端（Terminal），输入以下命令后回车，如需要，请输入密码

` sudo xattr -r -d com.apple.quarantine <path> `

> 注：<path>为应用程序路径，直接从文件夹目录拖拽即可自动填写<path>


##### 解决方案3.

 找到 `iOS/Flutter` 文件夹，再找到以前备份的无报错代码替换掉文件夹内容，应该就不会报错了。
 
 再执行下 `flutter build ios --release` 
 编译过程中会重新生成新的  `iOS/Flutter` 文件夹下内容，覆盖我们替换的文件。
 
 ##### 以上解决方案有可能需要结合使用。