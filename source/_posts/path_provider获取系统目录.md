---
title: path_provider获取系统目录
categories:
  - Flutter
tags:
  - path_provider
abbrlink: 10017
date: 2019-10-13 15:22:25
---



### PathProvider 插件

 > PathProvider 访问设备文件系统上的常用位置。
 
 #### 使用方法：
 1. 在pubspec.yaml文件中添加 PathProvider 插件
  
    `path_provider: ^*.*.*`[查看最新版本](https://pub.dartlang.org/packages/path_provider)

 2. 在文件中导入：

    `import 'package:path_provider/path_provider.dart';`
 
 
 

1. `DocumentsDirectory`
   >  文档目录，用于存储只有自己可以访问的文件。只有当应用程序被卸载时，系统才会清除该目录。在`iOS`上，这对应于`NSDocumentDirectory`。在`Android`上，这是`AppData`目录。 

    `String docDir = (await getApplicationDocumentsDirectory()).path;`
    
2. `TemporaryDirectory`
    > 系统可随时清除的临时目录（缓存）。在`iOS`上，这对应于`NSTemporaryDirectory()` 返回的值。在`Android`上，这是`getCacheDir()`返回的目录。

    `String tempDir = (await getTemporaryDirectory()).path;`
    
3. `SupportDirectory`
    >在iOS上，它使用`NSApplicationSupportDirectory` 来获取目录。在Android上，这是`getFilesDir`返回的目录。

    `String supportDir = (await getApplicationSupportDirectory()).path;`
    
4. `ExternalStorageDirectory`
    > 获取存储卡路径,仅在`Android`上中有效，`iOS`系统无此方法，可以通过`Platform.isIOS`来判断当前系统是否是`iOS`系统

    `String extStorageDir = (await getExternalStorageDirectory()).path;`
    
    
[PathProvider->GitHub](https://github.com/flutter/plugins/tree/master/packages/path_provider)

[PathProvider->Pub](https://pub.dartlang.org/packages/path_provider)
