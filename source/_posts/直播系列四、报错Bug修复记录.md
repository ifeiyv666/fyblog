---
title: 直播系列四、报错Bug修复记录
categories:
  - iOS
tags:
  - 直播
abbrlink: 10029
date: 2019-11-08 12:04:12
---


1. ./build-ffmpeg.sh

```
xcrun -sdk iphoneos clang is unable to create an executable file.
C compiler test failed.

If you think configure made a mistake, make sure you are using the latest
version from Git. If the latest version fails, report the problem to the
ffmpeg-user@ffmpeg.org mailing list or IRC #ffmpeg on irc.freenode.net.
Include the log file "config.log" produced by configure as this will help
solve the problem.

```
解决方法：

    sudo xcode-select --switch /Applications/Xcode.app
    
2. armv7

[https://www.jianshu.com/p/2669370bee23](https://www.jianshu.com/p/2669370bee23)

```
 ./libavutil/arm/asm.S:50:9: error: unknown directive
        .arch armv7-a
        ^
```
删除`armv7compile-ffmpeg.sh`文件中 

```
FF_ALL_ARCHS_IOS8_SDK="armv7 arm64 i386 x86_64"

改为 FF_ALL_ARCHS_IOS8_SDK="arm64 i386 x86_64"
```