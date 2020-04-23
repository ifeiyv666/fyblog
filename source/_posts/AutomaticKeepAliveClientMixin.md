---
title: This method overrides a method annotated as @mustCallSuper in 'AutomaticKeepAliveClientMixin', but doesn't invoke the overridden method.
categories:
  - Flutter
tags:
  - Flutter的坑
  - AutomaticKeepAliveClientMixin
date: 2020-04-14 15:54:47
---


#### 使用`AutomaticKeepAliveClientMixin` 警告⚠️ `This method overrides a method annotated as @mustCallSuper in 'AutomaticKeepAliveClientMixin', but doesn't invoke the overridden method.`

>该方法将覆盖在'AutomaticKeepAliveClientMixin'中标注为@mustCallSuper的方法，但不会调用覆盖的方法。

解决方案： 

 1. 检查 添加AutomaticKeepAliveClientMixin
 2. 添加 
 
    ```dart
    @override <br>
    bool get wantKeepAlive => true;
    ```
 3. build方法中记得调用父类方法`super.build(context);`
 
    ```dart
    Widget build(BuildContext context) {
        super.build(context);
        return Container();
    }
    ```
