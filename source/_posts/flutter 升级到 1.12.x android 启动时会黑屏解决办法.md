---
title: flutter 升级到 1.12.x android 启动时会黑屏解决办法
categories: Flutter
tags:
  - Flutter黑屏
  - Android黑屏
  - flutter 1.12.x
abbrlink: 10155
date: 2020-04-23 13:33:20
---

flutter 升级到 1.12.x android 启动时会黑屏解决办法

1. 直接用flutter 1.12.x SDK创建的项目

   需要修改`AndroidManifest.xml`文件，修改如下：

   ```java
   <application
           android:name="io.flutter.app.FlutterApplication"
           android:label="ifeiyv"
           android:icon="@mipmap/ic_launcher">
           <activity
               android:name=".MainActivity"
               android:launchMode="singleTop"
               android:theme="@style/LaunchTheme"
               android:configChanges="orientation|keyboardHidden|keyboard|screenSize|smallestScreenSize|locale|layoutDirection|fontScale|screenLayout|density|uiMode"
               android:hardwareAccelerated="true"
               android:windowSoftInputMode="adjustResize">
                 //
               <meta-data
                   android:name="io.flutter.embedding.android.SplashScreenDrawable"
                   android:resource="@drawable/launch_background"
                   />
               <meta-data
                   android:name="io.flutter.embedding.android.NormalTheme"
                   android:resource="@drawable/launch_background"
                   />
               <intent-filter>
                   <action android:name="android.intent.action.MAIN"/>
                   <category android:name="android.intent.category.LAUNCHER"/>
               </intent-filter>
           </activity>
           <!-- Don't delete the meta-data below.
                This is used by the Flutter tool to generate GeneratedPluginRegistrant.java -->
           <meta-data
               android:name="flutterEmbedding"
               android:value="2" />
       </application>
   ```

   如果存在`meta-data` 的 `android:name="io.flutter.app.android.SplashScreenUntilFirstFrame"`，删除此`meta-data`，添加如下代码：

   ```java
     <meta-data
          android:name="io.flutter.embedding.android.SplashScreenDrawable"
          android:resource="@drawable/launch_background"
      />
      <meta-data
          android:name="io.flutter.embedding.android.NormalTheme"
          android:resource="@drawable/launch_background"
       />
   ```

   修改launch_background.xml，这个要根据需求添加开屏视图

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <!-- Modify this file to customize your launch splash screen -->
   <layer-list xmlns:android="http://schemas.android.com/apk/res/android">
       <item
            android:left="0dp"
            android:top="0dp"
            android:bottom="0dp"
            android:right="0dp"
           android:drawable="@drawable/pic_bg" />
       <!-- You can insert your own image assets here -->  
   </layer-list>
   
   ```

   在`<application>`标签下添加新的 `<meta-data>` ,一旦您在AndroidManifest中进行了声明并使用了插件，能够使用使用了新的Android的插件（将插件注册为，`FlutterEngine`而不是`PluginRegistry.Registrar`

   ```xml
   < meta-data 
       android ：name = “flutterEmbedding”
       android ：value = “2” />
   ```

   

2. 如果是低版本创建的项目升级,除了以上修改外还需要修改以下内容：

   ```java
   //FlutterActivity包路径修改
   //把
   import io.flutter.app.FlutterActivity;
   //修改为
   import io.flutter.embedding.android.FlutterActivity;
   ```

   

   以前 

   ```java
   import io.flutter.app.FlutterActivity;
   import io.flutter.plugins.GeneratedPluginRegistrant;
   
   public class MainActivity extends FlutterActivity {
     @Override
     protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       GeneratedPluginRegistrant.registerWith(this);
     }
   
     // ...some amount of custom code for your app is here.
   }
   ```

   现在

   ```java
   import androidx.annotation.NonNull;
   import io.flutter.embedding.android.FlutterActivity;
   import io.flutter.embedding.engine.FlutterEngine;
   import io.flutter.plugins.GeneratedPluginRegistrant;
   
   public class MainActivity extends FlutterActivity {
     @Override
     public void configureFlutterEngine(@NonNull FlutterEngine flutterEngine) {
       GeneratedPluginRegistrant.registerWith(flutterEngine);
     }
   }
   ```

3. 这里仅有修复黑屏的问题，更多升级详细信息请前往	***官方升级指南 -》***  [前往](https://github.com/flutter/flutter/wiki/Upgrading-pre-1.12-Android-projects)  