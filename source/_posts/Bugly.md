---
title: iOS Bugly集成
categories:
  - iOS
abbrlink: 11113
tags:
  - Bugly
  - dSYM符号表
date: 2020-05-26 11:22:34

---



# Bugly iOS SDK 使用指南

## SDK 集成

Bugly提供两种集成方式供iOS开发者选择：

- 通过CocoaPods集成
- 手动集成

如果您是从`Bugly 2.0`以下版本升级过来的，请查看[iOS SDK 升级指南](https://bugly.qq.com/docs/user-guide/upgrading-2.x-ios/)

> Bugly iOS SDK 最低兼容系统版本 **iOS 7.0**

#### 通过CocoaPods集成

在工程的`Podfile`里面添加以下代码：

```
pod 'Bugly'
```

保存并执行`pod install`,然后用后缀为`.xcworkspace`的文件打开工程。

> 注意:
>
> **命令行下执行`pod search Bugly`,如显示的`Bugly`版本不是最新的，则先执行`pod repo update`操作更新本地repo的内容**
>
> 关于`CocoaPods`的更多信息请查看 [CocoaPods官方网站](https://cocoapods.org/)。

#### 手动集成

- 下载 [Bugly iOS SDK](https://bugly.qq.com/docs/release-notes/release-ios-bugly/)
- 拖拽`Bugly.framework`文件到Xcode工程内(请勾选`Copy items if needed`选项)
- 添加依赖库
  - `SystemConfiguration.framework`
  - `Security.framework`
  - `libz.dylib` 或 `libz.tbd`
  - `libc++.dylib` 或 `libc++.tbd`



## 初始化SDK

#### 导入头文件

在工程的`AppDelegate.m`文件导入头文件

> ```objective-c
> #import <Bugly/Bugly.h>
> ```
>
> **如果是`Swift`工程，请在对应`bridging-header.h`中导入**

#### 初始化Bugly

在工程`AppDelegate.m`的`application:didFinishLaunchingWithOptions:`方法中初始化：

- **Objective-C**

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [Bugly startWithAppId:@"此处替换为你的AppId"];
    return YES;
}
```

- **Swift**

```swift
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
    Bugly.startWithAppId("此处替换为你的AppId")
    return true
}
```



# Bugly iOS 符号表配置（可选）

## 介绍

### 什么是符号表？

符号表是内存地址与函数名、文件名、行号的映射表。符号表元素如下所示：

```
<起始地址> <结束地址> <函数> [<文件名:行号>]
```

### 为什么要配置符号表？

为了能快速并准确地定位用户APP发生**Crash的代码位置**，Bugly使用**符号表**对APP发生Crash的程序**堆栈**进行**解析**和**还原**。

举一个例子：

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/4001.png?v=20200312155538)

**Bugly提供了自动和手动两种方法配置iOS符号表。**

## 自动配置：XCode + sh脚本

自动配置请首先下载和解压[自动配置符号表工具包](https://bugly.qq.com/v2/sdk?id=6ecfd28d-d8ea-4446-a9c8-13aed4a94f04)，然后选择上传方式并配置Xcode的编译执行脚本。

### 上传方式

使用脚本自动配置支持两种上传方式：

- 方式一：直接上传dSYM文件（默认方式 ）
- 方式二：提取dSYM文件的符号表文件并上传

其中，使用方式二需要额外操作以下几步：

- 下载符号表提取工具依赖的[Java运行环境](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)（JRE或JDK版本需要>=1.6）
- 把工具包`buglySymbolIOS.jar`保存在用户主目录（Home）的`bin`目录下（没有`bin`文件夹,请自行创建）:

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/4006.png?v=20200312155538)



### 配置Xcode编译执行脚本

- 在Xcode工程对应Target的`Build Phases`中新增`Run Scrpit Phase`

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/4002.jpg?v=20200312155538)

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/4003.jpg?v=20200312155538)

- 打开工具包中的`dSYM_upload.sh`，复制所有内容，在新增的`Run Scrpit Phase`中粘贴
- 修改新增的`Run Scrpit`中的 `<YOUR_APP_ID>` 为您的App ID，`<YOUR_APP_KEY>`为您的App Key，`<YOUR_BUNDLE_ID>` 为App的Bundle Id

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/4004.jpg?v=20200312155538)

脚本默认在**Debug**模式及**模拟器编译**情况下不会上传符号表，在需要上传的时候，请修改下列选项

- Debug模式编译是否上传，1＝上传 0＝不上传，默认不上传

  `UPLOAD_DEBUG_SYMBOLS=0`

- 模拟器编译是否上传，1＝上传 0＝不上传，默认不上传

  `UPLOAD_SIMULATOR_SYMBOLS=0`

至此，自动上传符号表脚本配置完毕，Bugly 会在每次 Xcode 工程编译后自动完成符号表配置工作。

## 手动配置

手动配置的流程如下：

- 下载最新版**[Bugly iOS符号表工具](https://bugly.qq.com/v2/sdk?id=37f16cf0-2020-4e30-9e8d-0f7de59cfe94)**，其中工具包中包括：
  - 符号表工具JAR包（buglySymboliOS.jar）
  - Windows的脚本（buglySymboliOS.bat）
  - Shell脚本（buglySymboliOS.sh）
  - 默认符号表配置文件（settings.txt）
  - 符号表工具iOS版-使用指南
- 根据Crash的UUID定位dSYM文件
- 使用工具生成符号表文件（zip文件）
- 在页面上传符号表文件

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/4007.png?v=20200312155538)

**其他说明**

- Bugly iOS符号表工具2.3.0及以上版本增加了上传功能，2.5.0及以上版本支持dSYM文件的上传；
- 定位dSYM文件的方法和工具的使用方法请参考：“符号表工具iOS版-使用指南”。

## 符号表上传接口

Bugly提供了上传符号表的API接口（使用**POST**方式上传）:

- https://api.bugly.qq.com/openapi/file/upload/symbol

HTTPS接口支持上传dSYM文件（需要压缩成Zip文件）和符号表文件（Symbol）。



#### 参数说明

上传接口的参数说明如下：

| 属性           | 说明                   |
| -------------- | ---------------------- |
| api_version    | API版本，固定为1       |
| app_id         | App ID                 |
| app_key        | App Key                |
| symbolType     | 符号表类型，iOS为2     |
| bundleId       | 包名（Package）        |
| productVersion | 版本号（Version Name） |
| fileName       | 符号表文件名           |
| file           | 符号表文件             |

**其中包名、版本号和符号表文件名需要做URL Encode。**

#### 例子：使用Curl上传

使用Curl工具来上传的例子如下：

- 上传dSYM文件

```
curl -k "https://api.bugly.qq.com/openapi/file/upload/symbol?app_key=xxxxxx&app_id=xxxxxx" --form "api_version=1" --form "app_id=xxxxxx" --form "app_key=xxxxxx" --form "symbolType=2"  --form "bundleId=com.demo.test" --form "productVersion=1.0" --form "channel=xxx" --form "fileName=app.dSYM.zip" --form "file=@app.dSYM.zip" --verbose
```

- 上传符号表文件（Symbol文件）

```
curl -k "https://api.bugly.qq.com/openapi/file/upload/symbol?app_key=xxxxxx&app_id=xxxxxx" --form "api_version=1" --form "app_id=xxxxxx" --form "app_key=xxxxxx" --form "symbolType=2"  --form "bundleId=com.demo.test" --form "productVersion=1.0" --form "fileName=symbol.zip" --form "file=@symbol.zip" --verbose
```

## dSYM文件

### 什么是dSYM文件？

iOS平台中，dSYM文件是指具有调试信息的目标文件，文件名通常为：**xxx.app.dSYM**。如下图所示：

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/dSYM.png?v=20200312155538)

```
为了方便找回Crash对应的dSYM文件和还原堆栈，建议每次构建或者发布APP版本的时候，备份好dSYM文件。
```

### 如何定位dSYM文件？

一般情况下，项目编译完dSYM文件跟app文件在同一个目录下，下面以XCode作为IDE详细说明定位dSYM文件。

```
-> 进入XCode；
-> 打开工程（已编译过）；
-> 在左栏找到“Product”项；
-> 鼠标右键点击编译生成的“xxx.app”；
-> 点击“Show in Finder”；
```

如下图所示：

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/finder.png?v=20200312155538)

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/finder_dsym.png?v=20200312155538)

**`如果有多个dSYM文件，可以在使用工具时指定输入为dSYM文件所在的目录或者工程目录。`**

### XCode编译后没有生成dSYM文件？

XCode Release编译默认会生成dSYM文件，而Debug编译默认不会生成，对应的Xcode配置如下：

```
XCode -> Build Settings -> Code Generation -> Generate Debug Symbols -> Yes
XCode -> Build Settings -> Build Option -> Debug Information Format -> DWARF with dSYM File
```

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/xcode.png?v=20200312155538)

### 开启Bitcode之后需要注意哪些问题？

- 在点“Upload to App Store”上传到App Store服务器的时候需要声明符号文件（dSYM文件）的生成：

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/BitcodedSYM-0.jpg?v=20200312155538)

- 在配置符号表文件之前，需要从App Store中把该版本对应的dSYM文件下载回本地（参考“[如何找回已发布到App Store的App对应的dSYM文件？](https://bugly.qq.com/docs/user-guide/symbol-configuration-ios/?v=20200312155538#app-storeappdsym)”），然后用符号表工具生成和上传符号表文件。
- 不需要配置自动生成符号表的脚本了，也不要用本地生成的dSYM文件来生成符号表文件，因为本地编译生成的dSYM文件的符号表信息都被隐藏了。如果用本地编译生成的dSYM文件生成符号表文件并配置到Bugly平台之后，还原出来的结果将是类似于“__hiden#XXX”这样的符号。

### 如何判断dSYM文件是否与Crash的UUID匹配？

Bugly还原Crash堆栈时，需要根据UUID来匹配符号表文件，因此只有上传的符号表文件的UUID与Crash对应APP的UUID一致时，才能准确地对堆栈进行还原。

- 查看符号表文件的UUID（“[如何查看dSYM文件的UUID？](https://bugly.qq.com/docs/user-guide/symbol-configuration-ios/?v=20200312155538#dsymuuid)”）
- 查看Crash对应的APP的UUID

**Bugly v1.0页面**

```
崩溃 ---> Crash issue ---> dSYM UUID
```

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/UUID_1.png?v=20200312155538)

**Bugly v2.0页面**

```
崩溃分析 ---> Crash issue ---> 符号表 ---> UUID
```

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/UUID_2.png?v=20200312155538)

### 如何查看dSYM文件的UUID？

#### 通过命令查看UUID

```
xcrun dwarfdump --uuid <dSYM文件>
```

#### 通过符号表文件查看UUID

符号表文件的UUID与dSYM文件的UUID是一致的，因此可以通过符号表工具生成的符号表文件来查看dSYM文件的UUID：

```
生成符号表文件(.zip) ---> 解压符号表文件(.symbol) ---> 使用文本编辑器打开符号表文件
```

![Alt text](https://bugly.qq.com/docs/img/symbol-ios/UUID.png?v=20200312155538)

其中符号表文件的“UUID”信息即Debug SO文件的UUID，亦是符号表文件的UUID，如果文件较大，建议使用“Sublime Text”等文本编辑器来打开符号表文件。

### 如何找回已发布到App Store的App对应的dSYM文件？

#### 通过Xcode找回

1. 打开 Xcode 顶部菜单栏 -> Window -> Organizer 窗口： ![Alt text](https://bugly.qq.com/docs/img/symbol-ios/BitcodedSYM-1.jpg?v=20200312155538)
2. 打开 Xcode 顶部菜单栏，选择 Archive 标签： ![Alt text](https://bugly.qq.com/docs/img/symbol-ios/BitcodedSYM-2.jpg?v=20200312155538)
3. 找到发布的归档包，右键点击对应归档包，选择Show in Finder操作： ![Alt text](https://bugly.qq.com/docs/img/symbol-ios/BitcodedSYM-4.jpg?v=20200312155538)
4. 右键选择定位到的归档文件，选择显示包内容操作： ![Alt text](https://bugly.qq.com/docs/img/symbol-ios/BitcodedSYM-5.jpg?v=20200312155538)
5. 选择dSYMs目录，目录内即为下载到的 dSYM 文件： ![Alt text](https://bugly.qq.com/docs/img/symbol-ios/BitcodedSYM-6.jpg?v=20200312155538)

#### 通过iTunes Connect找回

1. 登录[iTunes Connect](https://itunesconnect.apple.com/)；
2. 进入“我的App（My Apps）”的“活动（Activity）”页面： ![Alt text](https://bugly.qq.com/docs/img/symbol-ios/ic-1.png?v=20200312155538)
3. 在“所有构件版本（All Builds）”中选择某一个版本，点“下载dSYM（Download dSYM）”下载dSYM文件： ![Alt text](https://bugly.qq.com/docs/img/symbol-ios/ic-2.png?v=20200312155538)

#### 通过mdfind工具找回

在Bugly的issue页面查询到crash对应的UUID：

然后在Mac的Shell中，用mdfind命令定位dSYM文件：

```
mdfind "com_apple_xcode_dsym_uuids == <UUID>"
```

> 注意，使用mdfind时，UUID需要格式转换（增加“-”）： 12345678-1234-1234-1234-xxxxxxxxxxxx

例如，要定位的dSYM的UUID为：E30FC309DF7B3C9F8AC57F0F6047D65F 则定位dSYM文件的命令如下：

```
mdfind "com_apple_xcode_dsym_uuids == E30FC309-DF7B-3C9F-8AC5-7F0F6047D65F"
                                     |12345678-1234-1234-1234-xxxxxxxxxxxx|
```

**建议每次构建或者发布APP版本的时候，备份App对应的dSYM文件！**



### 开启debug模式符号表上传功能（主要用于测试集成问题，可不需要）

XCode编译后生成dSYM文件设置

XCode Release编译默认会生成dSYM文件，而Debug编译默认不会生成，对应的Xcode配置如下：

- XCode -> Build Settings -> Code Generation -> Generate Debug Symbols -> Yes

- XCode -> Build Settings -> Build Option -> Debug Information Format -> DWARF with dSYM File
- 脚本中 UPLOAD_DEBUG_SYMBOLS的值改为1

> 不需要debug模式上传的话，只需要还原到之前的设置就行了



官方文档地址 ：[Bugly iOS SDK 使用指南](https://bugly.qq.com/docs/user-guide/instruction-manual-ios/?v=20200312155538)  [Bugly iOS 符号表配置](https://bugly.qq.com/docs/user-guide/symbol-configuration-ios/?v=20200312155538) 





#### 通过bug报错的堆栈信息 和 符号表结合解析后能够快速的定位到类、方法甚至行号

![bugly](bugly.png)



