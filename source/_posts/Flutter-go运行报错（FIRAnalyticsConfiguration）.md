---
title: Flutter-go运行报错（FIRAnalyticsConfiguration）
categories:
  - Flutter
tags:
  - Flutter-go
  - Flutter的坑
abbrlink: 10006
date: 2019-07-19 21:48:12
---


### flutter go 项目下载后，运行报如下错误：


```$ flutter run
Launching lib/main.dart on iPhone Xʀ in debug mode...
Running Xcode build...                                                  
                                                   
Xcode build done.                                            3.3s
Failed to build iOS app
Error output from Xcode build:
↳
    ** BUILD FAILED **


Xcode's output:
↳
    === BUILD TARGET firebase_analytics OF PROJECT Pods WITH CONFIGURATION Debug ===
    /Users/l/Documents/flutter/.pub-cache/hosted/pub.dartlang.org/firebase_analytics-2.1.1+2/ios/Classes/FirebaseAnalyticsPlu
    gin.m:60:7: error: use of undeclared identifier 'FIRAnalyticsConfiguration'
        [[FIRAnalyticsConfiguration sharedInstance] setAnalyticsCollectionEnabled:[enabled boolValue]];
          ^
    1 error generated.

Could not build the application for the simulator.
Error launching application on iPhone Xʀ.

```

**解决方案：**

***
将根目录下`pubspec.yaml`文件中 `firebase_analytics: ^2.0.2+1` 改为 `firebase_analytics: ^3.0.1` 之后运行flutter run
***

*执行通过*