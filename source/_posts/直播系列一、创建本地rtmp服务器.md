---
title: 直播系列一、创建本地rtmp服务器
categories:
  - iOS
tags:
  - 直播
abbrlink: 10026
date: 2019-11-08 10:32:25
---


#### 在网上搜索参考了大量文章，解决了N多Bug,终于实现了直播功能

>nginx是非常优秀的开源服务器，用它来做hls或者rtmp流媒体服务器是非常不错的选择

#### 1、安装Homebrow

（1）执行克隆命令,github的项目(https://github.com/denji/homebrew-nginx)

    brew tap denji/nginx

> 注意`brew tap homebrew/nginx`报下面的错误,`homebrew/nginx`已经弃用. 报错：`Error: homebrew/nginx was deprecated. This tap is now empty as all its formulae were migrated`.

（2）执行安装命令:

    brew install nginx-full --with-rtmp-module  

（3）至此nginx和rtmp模块就安装好了，下面开始来配置nginx的rtmp模块
 接下来看一下nginx安装在什么地方:

     brew info nginx-full  

*打印信息*
```
The default port has been set in /usr/local/etc/nginx/nginx.conf to 8080 so that
nginx can run without sudo.

nginx will load all files in /usr/local/etc/nginx/servers/.

- Tips -
Run port 80:
 $ sudo chown root:wheel /usr/local/opt/nginx-full/bin/nginx
 $ sudo chmod u+s /usr/local/opt/nginx-full/bin/nginx
Reload config:
 $ nginx -s reload
Reopen Logfile:
 $ nginx -s reopen
Stop process:
 $ nginx -s stop
Waiting on exit process
 $ nginx -s quit

To have launchd start denji/nginx/nginx-full now and restart at login:
  brew services start denji/nginx/nginx-full
Or, if you don't want/need a background service you can just run:
  nginx
```

nginx安装所在位置:

     /usr/local/opt/nginx-full/bin/nginx

nginx配置文件所在位置:

    /usr/local/etc/nginx/nginx.conf

（4）启动nginx,执行命令:

    sudo  nginx
    
#### 2、测试nginx：

    在浏览器中打开如下地址：http://localhost:8080入过

如果出现`Welcome to nginx!`,说明安装成功.

如果终端上提示：

    nginx: [emerg] bind() to 0.0.0.0:8080 failed (48: Address already in use)  

则表示8080端口被占用了, 查看端口PID

    lsof -i tcp:8080  

kill掉占用8080端口的PID

    kill 9603（这里替换成占用8080端口的PID）  

#### 3、重新加载nginx的配置文件

（1）修改nginx.conf这个配置文件，配置rtmp
 复制nginx配置文件所在位置:

    vi /usr/local/etc/nginx/nginx.conf  

（2）执行上面命令会直接编辑,或者直接前往当前文件用记事本打开.
 滚动到最后面(最后一个}后面即可，不能在{}里面)，添加一下代码，进行配置，最后记得保存。

```
rtmp {  
  server {  
      listen 1935;  
    #直播流配置  
      application rtmplive {  
          live on;  
          #为 rtmp 引擎设置最大连接数。默认为 off  
          max_connections 1024;  
       }  
      application hls{  
          live on;  
          hls on;  
          hls_path /usr/local/var/www/hls;  
          hls_fragment 1s;  
      }  
   }  
}  
```

（3）编辑完成之后,执行一下重新加载配置文件命令:

    sudo nginx -s reload

>需要输入开机密码 sudo不加的话会报错： `nginx: [alert] could not open error log file: open() "/usr/local/var/log/nginx/error.log" failed (13: Permission denied)`该命令执行后会出来一个弹框询问是否允许 nginx 加入到网络中，选择允许即可。

（4）重启nginx：

    sudo /usr/local/opt/nginx-full/bin/nginx -s reload  

PS：如果你之前不是按照我上面的方法按照的 nginx，在执行 sudo nginx -s reload 时报了如下错，建议你卸载 nginx后按照我上面的步骤重新安装nginx。
 nginx: [emerg] unknown directive "rtmp" in /usr/local/etc/nginx/nginx.conf:119

**nginx常用方法:**
>出现权限不足的错误提示时，命令前加上 sudo
```
重新加载配置文件:  nginx -s reload
重新加载日志:     nginx -s reopen 
停止 nginx:      nginx -s stop  
有序退出 nginx:   nginx -s quit  
```

#### 4、安装ffmepg工具

    brew install ffmpeg

#### 5、本地推流

(1)、搭建本地视频直播，比如电脑上面有很多电影，我们可以通过推流的形式实现实时直播：

A：在电脑上播放推流内容
 安装一个支持rtmp协议的视频播放器，Mac下可以用VLC
 下载[VLC](http://soft.macx.cn/3164.htm)
 
 本地下载一个视频文件路径为 /Users/iOS002/Desktop/loginmovie.mp4
 
 执行以下命令:
 
     ffmpeg -re -i /Users/iOS002/Desktop/loginmovie.mp4  -vcodec libx264 -acodec aac -strict -2 -f flv rtmp://localhost:1935/rtmplive/room

用vlc 然后打开 VLC 中 的 file -- Open Network, 直接输入代码中的 url:

    rtmp://localhost:1935/rtmplive/room

即可以通过VLC来播放终端中实时推过来的 RTMP流。

B：通过手机观看电脑的推流
 
 通过集成 ijkplayer 把地址换成推流的地址即可观看
 
 播放端用的针对RTMP优化过的ijkplayer，ijkplayer是基于FFmpeg的跨平台播放器，这个开源项目已经被多个 App 使用，其中映客、美拍和斗鱼使用了 ijkplayer。
 

(2)、桌面录制或者分享

    ffmpeg -f avfoundation -i "1" -vcodec libx264 -preset ultrafast -acodec libfaac -f flv rtmp://localhost:1935/rtmplive/room 

(3)、桌面+麦克风

    ffmpeg -f avfoundation -i "1:0" -vcodec libx264 -preset ultrafast -acodec libmp3lame -ar 44100 -ac 1 -f flv rtmp://localhost:1935/rtmplive/room

(4)、桌面+麦克风，并且还要摄像头拍摄到自己

    ffmpeg -f avfoundation -framerate 30 -i "1:0" \-f avfoundation -framerate 30 -video_size 640x480 -i "0" \-c:v libx264 -preset ultrafast \-filter_complex 'overlay=main_w-overlay_w-10:main_h-overlay_h-10' -acodec libmp3lame -ar 44100 -ac 1 -f flv rtmp://localhost:2016/rtmplive/room  

#### 6、手机推流

可以用  LFLiveKit 集成到工程进行推流，LFLiveKit已经帮我们实现了视频采集、后台录制、美颜功能、支持h264、AAC编码，动态改变速率，RTMP传输等，我们开发的时候就很简单了只需把localhost:8080换成自己电脑的ip地址即可:

    rtmp://10.0.0.17:1935/rtmplive/room
注意通过网络查看电脑的局域网 IP替换掉 localhost 即可。

A：通过VLC观看手机的推流

 打开手机直播后，然后在电脑上打开VLC（同上），就能实现手机推流，在电脑上拉流播放了！！(注：手机需要和电脑连接同一网络！)

B：通过手机观看手机的推流（这也就是市面上的那些直播App的最终实现形式了）

 通过集成 ijkplayer 把地址换成推流的地址即可观看。
 

PS：一个很隐蔽的报错：

如果你发现你的推流地址和拉流地址在电脑上都是好好的，但是通过手机实现的时候就是报错，那么估计就是因为Mac防火墙的问题。

```
ERROR: PILI_RTMP_Connect0, failed to connect socket. 60 (Operation timed out)
ERROR: WriteN, PILI_RTMP send error 9, Bad file descriptor, (140 bytes)
ERROR: PILI_RTMP_Connect0, failed to connect socket. 60 (Operation timed out)
ERROR: WriteN, PILI_RTMP send error 9, Bad file descriptor, (140 bytes)
```

关闭 Mac 的防火墙即可解决问题。
    
    偏好设置->安全性与隐私->防火墙