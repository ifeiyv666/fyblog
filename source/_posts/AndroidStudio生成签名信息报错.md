---
title: AndroidStudio生成签名信息报错
categories:
  - Android
tags:
  - Android Studio
  - jks
abbrlink: 101001
date: 2020-02-05 14:33:46
---

#### AndroidStudio生成签名信息报错

```java
Key was created with errors:
Warning:
JKS 密钥库使用专用格式。建议使用 
"keytool -importkeystore -srckeystore
(存放路径)\AndroidSigh.jks -destkeystore
(存放路径)\AndroidSigh.jks -deststoretype pkcs12"
迁移到行业标准格式 PKCS12。

```

> 解决方案在终端中输入以下命令：

```java
keytool -genkey -alias (alias名称) -keypass (alias密码) -keyalg RSA -keysize 2048 -validity 36500 -keystore (存放路径)\(保存jks文件名称).jks -storepass (keyStore密码)

//然后根据提示信息填写即可（上面命令中的括号要删掉）

```


