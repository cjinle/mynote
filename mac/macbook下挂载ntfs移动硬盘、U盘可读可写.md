# macbook下挂载ntfs移动硬盘、U盘可读可写
相信很多用macbook的朋友，偶尔会用上移动硬盘，但一般人的移动硬盘格式都是ntfs的。
插到macbook下就只能读了，那是因为ntfs格式版权问题，这个时候一般安装`tuxera`之类的软件可以解决，
但软件是收费的，所以下面是一个免费的方法，使用起来也有点麻烦，主要是使用了`ntfs-3g`进行手动挂载

### 安装依赖的软件
```sh
brew cask install osxfuse
brew install ntfs-3g
```

### 手动挂载，以我的U盘为例
```
/Volumes/udisk $ df -lh
Filesystem     Size   Used  Avail Capacity iused               ifree %iused  Mounted on
/dev/disk1s1  113Gi   60Gi   51Gi    55% 1111527 9223372036853664280    0%   /
/dev/disk1s4  113Gi  1.0Gi   51Gi     2%       1 9223372036854775806    0%   /private/var/vm
/dev/disk2s1  3.7Gi  143Mi  3.6Gi     4%      48             3780064    0%   /Volumes/udisk

umount /Volumes/udisk
sudo mkdir /Volumes/NTFS
sudo /usr/local/bin/ntfs-3g /dev/disk2s1 /Volumes/NTFS -olocal -oallow_other
```

这样就挂载把U盘挂载到`/Volumes/NTFS`下了，下面可以测试一下读写就OK了。

### 自动挂载？
也是可以实现的，但涉及到替换系统命令，要在恢复模式下操作才可以，这个对一般用户来讲，太复杂了。
对系统来讲也有一定的风险，现在这个基本上可以实现，手动挂载一下就可以了

参考文档：https://github.com/osxfuse/osxfuse/wiki/NTFS-3G


### 查看当前系统的存储设备
```
/Volumes $ diskutil list
/dev/disk0 (internal, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *121.3 GB   disk0
   1:                        EFI EFI                     209.7 MB   disk0s1
   2:                 Apple_APFS Container disk1         121.1 GB   disk0s2

/dev/disk1 (synthesized):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      APFS Container Scheme -                      +121.1 GB   disk1
                                 Physical Store disk0s2
   1:                APFS Volume OS X Base System        64.7 GB    disk1s1
   2:                APFS Volume Preboot                 20.1 MB    disk1s2
   3:                APFS Volume Recovery                520.8 MB   disk1s3
   4:                APFS Volume VM                      1.1 GB     disk1s4

/dev/disk2 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *4.0 GB     disk2
   1:               Windows_NTFS udisk                   4.0 GB     disk2s1

```