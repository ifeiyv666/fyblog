---
title: Mac 文件已损坏或者未知开发者解决办法
categories:
  - Mac
tags:
  - 文件已损坏解决办法
  - 未知开发者解决办法
abbrlink: 10030
date: 2020-03-17 16:01:03
---


##### sudo spctl --master-disable (所有来源权限)


##### 各位注意，这是10.15以上系统的完美解决方法

##### 打开终端（Terminal），输入以下命令后回车，如需要，请输入密码

##### sudo xattr -r -d com.apple.quarantine <path>

> 注：<path>为应用程序路径，直接从文件夹目录拖拽即可自动填写<path>