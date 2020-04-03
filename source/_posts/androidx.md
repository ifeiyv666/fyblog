---
title: androidx
categories:
  - Android
tags:
  - Android
abbrlink: 10003
date: 2019-06-25 16:33:55
---


#### 1. ViewModelProviders


在`build.gradle` 的 `dependencies` 中加入

```java
implementation 'androidx.lifecycle:lifecycle-extensions:2.0.0'
```

在使用的地方导入：

```java
import androidx.lifecycle.ViewModelProviders;
```

即可使用：

``` java
myViewModel = ViewModelProviders.of(this).get(MyViewModel.class);

```

> 该方法 2.1.0 已弃用 ViewModelProviders.of() ,改为

```java
//导入 import androidx.lifecycle.ViewModelProvider;
myViewModel = ViewModelProvider(this).get(MyViewModel.class);

//或者
myViewModel = ViewModelProvider(getActivity()).get(MyViewModel.class);
```


#### 2. DataBinding

在 `build.gradle` 的  defaultConfig中加入 

```java
dataBinding{
    enabled true
}
```

`Sync Now`一下，把下面代码套在布局最外层，即可使用。

```java
<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">

    <data>

    </data>
    
    
    //============
    //这里写自己的布局
    
    
</layout>
```

