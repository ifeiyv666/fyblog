---
title: shared_preferences数据存储
categories:
  - Flutter
tags:
  - shared_preferences
abbrlink: 10018
date: 2019-10-19 18:52:45
---



### shared_preferences库

> shared_preferences库同时支持Android和ios平台,存键值对信息，进行数据本地持久化存储。

#### 引用方法

1. 在pubspec.yaml文件中添加依赖

    `shared_preferences: ^0.5.3+4`[->查看最新版本](https://pub.dev/packages/shared_preferences)

2. 执行$ flutter packages get命令 下载插件

3. 在使用的文件中导入：

    `import 'package:shared_preferences/shared_preferences.dart';`


#### 使用方法

```
      SharedPreferences sharedPreferences = await SharedPreferences.getInstance();

      sharedPreferences.setString("name", "hehe");
      sharedPreferences.setInt("age", 18);
      sharedPreferences.setDouble("height", 1.72);
      sharedPreferences.setBool("sex", true);//true 表示男 false表示女
      sharedPreferences.setStringList("like", ["MV","Music","Pic"]);
      
      print("=========get****("key")取出存储的数据==============");
      print("姓名:"+ sharedPreferences.getString("name"));
      print("年龄:" + sharedPreferences.getInt("age").toString());
      print("身高:"+ sharedPreferences.getDouble("height").toString());
      print("性别:"+ ((sharedPreferences.getBool("sex") == true) ? "男":"女"));
      print("爱好:"+ sharedPreferences.getStringList("like").toString());

      print("========getKeys()取出存储的所有key值=============");
      print(sharedPreferences.getKeys());
      
      print("========set***("key")给已经存在的key重新赋值=============");
      print("姓名:"+ sharedPreferences.getString("name"));
      sharedPreferences.setString("name", "feiyv");
      print("姓名:"+ sharedPreferences.getString("name"));
      
      print("========containsKey("key")判断存储的是否有某个Key值=============");
      print("name是否存在：" + sharedPreferences.containsKey("name"));
      print("rename是否存在：" + sharedPreferences.containsKey("rename"));
      
      print("========remove("key")删除单个Key数据=============");
      print("年龄:" + sharedPreferences.getInt("age").toString());
      sharedPreferences.remove("age");
      print("年龄:" + sharedPreferences.getInt("age").toString());
      
      print("========clear清除所有数据=============");
      sharedPreferences.clear();
      print("sharedPreferences.clear();");
      print("name是否存在：" + sharedPreferences.containsKey("name").toString());
      print("所有的key值："+ sharedPreferences.getKeys().toString());
```
#### 打印数据：

```

flutter: =========get****("key")取出存储的数据==============
flutter: 姓名:hehe
flutter: 年龄:18
flutter: 身高:1.72
flutter: 性别:男
flutter: 爱好:[MV, Music, Pic]

flutter: ========getKeys()取出存储的所有key值=============
flutter: {name, age, height, sex, like}

flutter: ========set****("key")给已经存在的key重新赋值=============
flutter: 姓名:hehe
flutter: 姓名:feiyv

flutter: ========containsKey("key")判断存储的是否有某个Key值=============
flutter: name是否存在：true
flutter: rename是否存在：false

flutter: ========remove("key")删除单个Key数据=============
flutter: 年龄:18
flutter: 年龄:null

flutter: ========clear清除所有数据=============
flutter: sharedPreferences.clear();
flutter: name是否存在：false
flutter: 所有的key值：{}

```

