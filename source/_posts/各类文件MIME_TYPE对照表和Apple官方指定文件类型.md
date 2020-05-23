---
title: 各类文件MIME_TYPE对照表和Apple官方指定文件类型
categories:
  - 收藏
abbrlink: 10156
tags:
  - MIME_TYPE
date: 2020-04-30 18:42:03
---





```ruby
 {".3gp",    "video/3gpp"},   
 {".apk",    "application/vnd.android.package-archive"},   
 {".asf",    "video/x-ms-asf"},   
 {".avi",    "video/x-msvideo"},   
 {".bin",    "application/octet-stream"},   
 {".bmp",    "image/bmp"},   
 {".c",  "text/plain"},   
 {".class",  "application/octet-stream"},   
 {".conf",   "text/plain"},   
 {".cpp",    "text/plain"},   
 {".doc",    "application/msword"},   
 {".docx",   "application/vnd.openxmlformats-officedocument.wordprocessingml.document"},   
 {".xls",    "application/vnd.ms-excel"},    
 {".xlsx",   "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"},   
 {".exe",    "application/octet-stream"},   
 {".gif",    "image/gif"},   
 {".gtar",   "application/x-gtar"},   
 {".gz", "application/x-gzip"},   
 {".h",  "text/plain"},   
 {".htm",    "text/html"},   
 {".html",   "text/html"},   
 {".jar",    "application/java-archive"},   
 {".java",   "text/plain"},   
 {".jpeg",   "image/jpeg"},   
 {".jpg",    "image/jpeg"},   
 {".js", "application/x-javascript"},   
 {".log",    "text/plain"},   
 {".m3u",    "audio/x-mpegurl"},   
 {".m4a",    "audio/mp4a-latm"},   
 {".m4b",    "audio/mp4a-latm"},   
 {".m4p",    "audio/mp4a-latm"},   
 {".m4u",    "video/vnd.mpegurl"},   
 {".m4v",    "video/x-m4v"},    
 {".mov",    "video/quicktime"},   
 {".mp2",    "audio/x-mpeg"},   
 {".mp3",    "audio/x-mpeg"},   
 {".mp4",    "video/mp4"},   
 {".mpc",    "application/vnd.mpohun.certificate"},          
 {".mpe",    "video/mpeg"},     
 {".mpeg",   "video/mpeg"},     
 {".mpg",    "video/mpeg"},     
 {".mpg4",   "video/mp4"},      
 {".mpga",   "audio/mpeg"},   
 {".msg",    "application/vnd.ms-outlook"},   
 {".ogg",    "audio/ogg"},   
 {".pdf",    "application/pdf"},   
 {".png",    "image/png"},   
 {".pps",    "application/vnd.ms-powerpoint"},   
 {".ppt",    "application/vnd.ms-powerpoint"},   
 {".pptx",   "application/vnd.openxmlformats-officedocument.presentationml.presentation"},   
 {".prop",   "text/plain"},   
 {".rc", "text/plain"},   
 {".rmvb",   "audio/x-pn-realaudio"},   
 {".rtf",    "application/rtf"},   
 {".sh", "text/plain"},   
 {".tar",    "application/x-tar"},      
 {".tgz",    "application/x-compressed"},    
 {".txt",    "text/plain"},   
 {".wav",    "audio/x-wav"},   
 {".wma",    "audio/x-ms-wma"},   
 {".wmv",    "audio/x-ms-wmv"},   
 {".wps",    "application/vnd.ms-works"},   
 {".xml",    "text/plain"},   
 {".z",  "application/x-compress"},   
 {".zip",    "application/x-zip-compressed"},   
 {"",        "*/*"} 
```



#### 官方指定的文件类型 Document Content Type UTIs 

[官方指定的文件类型](https://developer.apple.com/library/ios/documentation/Miscellaneous/Reference/UTIRef/Articles/System-DeclaredUniformTypeIdentifiers.html#//apple_ref/doc/uid/TP40009259-SW1)

```xml
	<array>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Viewer</string>
			<key>LSHandlerRank</key>
			<string>Owner</string>
			<key>CFBundleTypeIconFiles</key>
			<array/>
			<key>CFBundleTypeName</key>
			<string>文件共享</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>public.data</string>
				<string>com.microsoft.excel.xls</string>
				<string>public.text</string>
				<string>public.plain-text </string>
				<string>public.image</string>
				<string>public.jpeg</string>
				<string>public.png</string>
				<string>com.microsoft.bmp </string>
				<string>com.compuserve.gif </string>
				<string>com.adobe.pdf</string>
				<string>com.microsoft.powerpoint.ppt</string>
				<string>com.microsoft.word.doc</string>
			</array>
		</dict>
	</array>
```



