---
title: Mac下移动硬盘无法读取解决方案(以前是可以读取的)
categories:
  - Mac
abbrlink: 10155
tags:
  - Mac
  - 移动硬盘
date: 2020-05-08 11:28:30
---



#### Mac下移动硬盘无法读取(以前是可以读取的)

> 不进行处理的话，一般连接移动硬盘半个小时左右就会显示了；不想等待的话就执行以下命令，强制加载

可以在终端中执行以下命令：`diskutil list`  ,控制台输出信息如下：

```ruby
@ls--MacBook-Air  ~ $ diskutil list
/dev/disk0 (internal, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *121.3 GB   disk0
   1:                        EFI EFI                     209.7 MB   disk0s1
   2:                 Apple_APFS Container disk1         121.1 GB   disk0s2

/dev/disk1 (synthesized):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      APFS Container Scheme -                      +121.1 GB   disk1
                                 Physical Store disk0s2
   1:                APFS Volume Macintosh HD - 数据     95.8 GB    disk1s1
   2:                APFS Volume Preboot                 82.4 MB    disk1s2
   3:                APFS Volume Recovery                528.5 MB   disk1s3
   4:                APFS Volume VM                      3.2 GB     disk1s4
   5:                APFS Volume Macintosh HD            10.9 GB    disk1s5

/dev/disk2 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *1.0 TB     disk2
   1:                        EFI EFI                     209.7 MB   disk2s1
   2:       Microsoft Basic Data LPF                     1000.0 GB  disk2s2
```

通过以上输出信息，可以找到移动硬盘挂载路径：`/dev/disk2` ,根据输出显示实际挂载路径填写。

执行命令：`sudo diskutil mount /dev/disk2` ，控制台输出信息如下：

```ruby
@ls-MacBook-Air  ~ $ sudo diskutil mountDisk /dev/disk2
Volume(s) mounted successfully
```

输出以上信息表示移动硬盘挂载成功了，如果输出以下信息：

```ruby
 @ls-MacBook-Air  ~ $ sudo diskutil mount /dev/disk2
Password:
Volume on disk2 failed to mount
Perhaps the operation is not supported (kDAReturnUnsupported)
If it has a partitioning scheme, use "diskutil mountDisk"
If you think the volume is supported but damaged, try the "readOnly" option
```

输出以上信息表示不支持 `sudo diskutil mount /dev/disk2` 这种装载方式，使用以下方式进行装载

执行命令： `sudo diskutil mountDisk /dev/disk2 ` , 而不是  `sudo diskutil mount /dev/disk2`

```ruby
@ls-MacBook-Air  ~ $ sudo diskutil mountDisk /dev/disk2
Volume(s) mounted successfully
```



#### 以上命令方法不行的话，那就电脑连接移动硬盘老老实实等大概半个小时就好了



