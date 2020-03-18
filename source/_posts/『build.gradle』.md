---
title: 根目录下的build.gradle
categories:
  - Android
tags:
  - Android
  - android
  - flutter
abbrlink: 10000
date: 2019-06-16 12:11:32
---



#### 根目录下的build.gradle

```
// Top-level build file where you can add configuration options common to all sub-projects/modules.

buildscript {
    repositories {
        google()
        
        //代码托管库，设置后可以在项目中引用jcenter上的开源项目
        jcenter()
    }
    
    
    //引用anroid插件
    dependencies {
    
        //声明gradle插件，插件版本号
        classpath 'com.android.tools.build:gradle:3.5.3'
        
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        google()
        jcenter()
        
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}


```



#### app目录下的build.gradle

```

//声明是Android应用程序还是库模块
//com.android.appliccation 标识应用程序，可以直接运行
//com.android.library 标识这是一个库模块，依附于别的应用程序运行

apply plugin: 'com.android.application'


//配置项目构建的各种属性
android {

    //程序在编译时会检查lint，有任何错误提示会停止build，我们可以关闭这个开关
    lintOptions{
        //即使报错也不会停止打包
        abortOnError false
        //打包release版本的时候是否进行检测
        checkReleaseBuilds false
    }


    //编译SDK的版本，也就是API Level
    compileSdkVersion 28
    //build tools的版本，其中包括了打包工具aapt 、 dx
    //这个目录工具位于 sdk目录/build-tools/ 下
    buildToolsVersion '28.0.3'
    
    
    //关闭Android Studio的PNG合法性检查
    aaptOptions.cruncherEnabled = false
    aaptOptions.useNewCruncher = false
    
    //默认配置
    defaultConfig {
        //应用程序的包名
        applicationId "com.ifeiyv.android001"
        
        //最小的SDK版本，如果设置小于这个版本，或者大于maxSdkVersion将无法安装这个应用
        minSdkVersion 19
        
        //目标sdk版本，充分测试过的版本（建议版本）
        targetSdkVersion 28
        
        //版本号 每次更新增减
        versionCode 1
        
        //版本号，用户看到的版本号
        versionName "1.0"
        
        //指定打包成Jar文件时候的文件名称
        archivesBaseName = "demo-$versionName"
        
        
        //Native Development Kit
        //原生开发工具包是一组可以让您在Android应用中利用C和c++代码的工具,可用以从您自己的源代码构建,或者利用现有的预构建库.
        ndk{
            //设置（so）文件名称
            moduleName "testfeiyv"
            ldLibs "log","z","m","jnigraphics","android"
            
            //显示指定支持的ABIs
            abiFilters "armeabi","x86","armeabi-v7a"
            
            //C++11
            cFlags "-sd=c++11 -fexceptions"
            
            stl "gnustl_static"
        }
        
        //当方法数超过65535的时候允许打包成多个dex文件，动态加载dex
        //(方法的索引使用的是一个short值，而short最大值是65535)
        multiDexEnabled true
        
        //Instrumentation单元测试
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }
    
    sourceSets{
        main{
            //指定清单文件
            manifest.srcFile 'AndroidManifest.xml'
            //指定res资源目录
            res.srcDirs = ['res']
            //asset资源文件
            assets.srcDir  = ['assets']
            //jni代码目录
            jni.srcDirs 'src/main/jni'
            //jni库目录
            jniLibs.srcDir 'src/main/jniLibs'
            //指定Java源代码目录
            java.srcDirs = ['src']
            //指定resource目录
            resources.srcDirs = ['src']
            //指定aidl目录
            aidl.srcDirs = ['src']
            //指定source目录
            renderscript.srcDirs = ['src']
        }
        
        //指定debug模式的路径
        debug.setRoot('build-types/debug')
        //指定release模式的路径
        release.setRoot('build-types/release')
    }
    
    //mltiDex的一些相关配置，这样配置可以使编译速度更快
    dexOptions{
        //让它不要对Lib做preDexing
        preDexLibraries = fasle
        //开启incremental dexing,优化编译效率。这个功能Android Studio默认是关闭的
        incremental true
        //增加java堆内存大小
        javaMaxHeapSize "4g"
    }
    
    //签名配置
    signingConfigs{
        release{
            //密钥文件路径
            storeFile file("feiyv.keystore")
            //密钥文件密码
            storePassword "feiyvpwd"
            //key 别名
            keyAlias "fy"
            //key密码
            keyPassword "fypwd"
        }
        debug{
           //密钥文件路径
            storeFile file("feiyv.keystore")
            //密钥文件密码
            storePassword "feiyvpwd"
            //key 别名
            keyAlias "fy"
            //key密码
            keyPassword "fypwd" 
        }
    }
    
    
    //指定生成安装文件的配置，常有两个子包：release，debug，注：直接运行的都是debug安装文件
    buildTypes {
        //release版本的配置，即生成发布版文件的配置
        release {
            //是否支持zip
            zipAlignEnabled true
            //移除无用的resource文件
            shrinkResources true
            //是否对代码进行混淆，true标识混淆
            minifyEnabled false
            
            //指定混淆时使用的规则文件：
            //proguard-android.tex指所有项目通用的混淆规则，proguard-rules.pro当前项目特有的混淆规则
            //release的Proguard默认为Module下的proguard-rules.pro文件
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
            
            //是否支持调试
            debuggable false 
            
            //ndk的一些配置
            ndk {
                 // cFlags "-std=c++11 -fexceptions -O3 -D__RELEASE__" // C++11
                 // platformVersion = "19"
                 moduleName "hebbewifisafe" // 设置库(so)文件名称
                ldLibs "log", "z", "m", "jnigraphics", "android"
                 // 引入库，比如要用到的__android_log_print
                 abiFilters "armeabi", "x86", "armeabi-v7a"// "x86"
                 cFlags "-std=c++11 -fexceptions" // C++11
                 stl "gnustl_static"
             }
                // 采用动态替换字符串的方式生成不同的 release.apk （3.0之后版本的修改方式）
             applicationVariants.all { variant ->
                 variant.outputs.all { output ->
                     if (!variant.buildType.isDebuggable()) {
                         // 获取签名的名字 variant.signingConfig.name
                         // 要被替换的源字符串
                        def sourceFile = "app-release";
                         // 替换的字符串
　　　　　　　　　　　　　　　def replaceFile = "Demo-V${variant.versionName}.${releaseTime()}"
　　　　　　　　　　　　　　　outputFileName = output.outputFile.name.replace(sourceFile, replaceFile)
                     }
                 }
             }
             jniDebuggable false  // 关闭jni调试
        }
        debug { // debug版本的配置
            minifyEnabled false
             zipAlignEnabled true
             shrinkResources true // 移除无用的resource文件
             proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
             debuggable true
 //          jniDebuggable true
             ndk {
                 cFlags "-std=c++11 -fexceptions -g -D __DEBUG__" // C++11
             }
             jniDebuggable true
         }
 
    }
    
    
    
    productFlavors{
        //这里可以设置产品发布的一些东西
        //比如一种软件要发布到不同的渠道
        //且不同渠道中的包名不同，可以在此处
        //甚至可以设置不同的AndroidManifest.xml
        tencent{
            
        }
        huanwei{
            
        }
        all{
            
        }
    }
    
    
    // 所谓ProductFlavors其实就是可定义的产品特性，
    // 配合 manifest merger 使用的时候就可以达成在一次编译
    // 过程中产生多个具有自己特性配置的版本。
    // 这个配置的作用就是，为每个渠道包产生不同的 UMENG_CHANNEL_VALUE 的值。
    productFlavors.all{
        flavor -> flavor.manifestPlaceholder = [UMENG_CHANNEL_VALUE:name]
    }
    
 
 
 // 指定当前项目的所有依赖关系：本地依赖、库依赖、远程依赖
 // 本地依赖：可以对本地 Jar 包或目录添加依赖关系
 // 库依赖：可以对项目中的库模块添加依赖关系
 // 远程依赖：可以对 jcenter 库上的开源项目添加依赖
 // 标准的远程依赖格式是 域名:组织名:版本号
 
dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'com.android.support:recyclerview-v7:28.0.0'
//    implementation 'androidx.appcompat:appcompat:1.0.2'
//    implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
    testImplementation 'junit:junit:4.12'
//    androidTestImplementation 'androidx.test.ext:junit:1.1.0'
//    androidTestImplementation 'androidx.test.espresso:espresso-core:3.1.1'

}


 // 声明是要使用谷歌服务框架
 apply plugin: 'com.google.gms.google-services'
 
 
 // 第三方依赖库的本地缓存路径
 task showMeCache << {
     configurations.compile.each { println it }
 }
 
// 使用maven仓库。android有两个标准的library文件服务器，一个jcenter一个maven。两者毫无关系。
// jcenter有的maven可能没有，反之亦然。
// 如果要使用jcenter的话就把mavenCentral()替换成jcenter()
repositories {
     mavenCentral()
}
 
 
 def releaseTime() {
   return new Date().format("MMdd.HHmm")
}

```