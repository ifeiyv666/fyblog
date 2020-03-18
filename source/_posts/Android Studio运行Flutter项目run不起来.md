---
title: Android Studio运行Flutter项目run不起来
categories:
  - Android
tags:
  - Android
  - Flutter
abbrlink: 10002
date: 2019-06-19 14:46:56
---





#### 解决方案：

1. 修改`Flutter SDK`中的`flutter.gradle`文件,通过 `flutter>packages>flutter_tools>gradle>flutter.gradle`(注意这是Flutter SDK安装位置不是Android Studio的)路径找到`flutter.gradle`，打开`flutter.gradle`文件，修改配置：

注释掉`google()`和`jcenter()`,加入阿里的配置项

    maven {url 'https://maven.aliyun.com/repository/google'}
    maven {url 'https://maven.aliyun.com/repository/jcenter'}
    maven {url 'https://maven.aliyun.com/nexus/content/groups/public'}
   
 修改后：
 
    buildscript {
        repositories {
            //注释掉 google()和jcenter()
            // google()
            // jcenter()
        	maven {url 'https://maven.aliyun.com/repository/google'}
        	maven {url 'https://maven.aliyun.com/repository/jcenter'}
        	maven {url 'https://maven.aliyun.com/nexus/content/groups/public'}
        }
        dependencies {
            classpath 'com.android.tools.build:gradle:3.2.1'
        }
    }

2. 手动下载`gradle`进行配置
    
   找到创建的flutter项目：

   通过路径`flutterdemo001/android/gradle/wrapper/gradle-wrapper.properties`找到对应文件打开后：


    #Fri Jun 23 08:50:38 CEST 2017
    distributionBase=GRADLE_USER_HOME
    distributionPath=wrapper/dists
    zipStoreBase=GRADLE_USER_HOME
    zipStorePath=wrapper/dists
    distributionUrl=https\://services.gradle.org/distributions/gradle-4.10.2-all.zip
    
    
  找到`distributionUrl`对应的地址`https://services.gradle.org/distributions/gradle-4.10.2-all.zip`就是gradle的下载地址,注意文件中https后面有个`\`,复制到浏览器记得要删掉
   
   点击下载 [gradle-4.10.2-all.zip](https://services.gradle.org/distributions/gradle-4.10.2-all.zip)
   
   点击下载[其他版本gradle](http://services.gradle.org/distributions/)
   
   
   下载完成后，进行解压。
   然后打开目录：`Macintosh HD 》 用户 》当前登录用户名称》.gradle》wrapper》dists`⁩,
   可能有些电脑未打开隐藏文件可见，是看不到`.gradle`文件夹的,它是一个隐藏文件夹。
   使用快捷键`shift+command+.`来切换隐藏文件可见还是隐藏。找到dists文件夹后，把解压后的`gradle`拷贝一份放到dists文件夹下即可。
   

