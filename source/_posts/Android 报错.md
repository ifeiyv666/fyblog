---
title: Android报错
categories:
  - Android
tags:
  - Android
  - android
abbrlink: 10001
date: 2019-06-17 10:30:22
---




##### 1.**MISSING ACCESSIBILITY LABEL: WHERE MINSDK < 17, YOU SHOULD PROVIDE AN ‘ANDROID:HINT’ **

> 在布局文件（默认为main_activity.xml）添加
      
    xmlns:tools="http://schemas.android.com/tools"
      
    tools:ignore="LabelFor"
        

