# macbook制作linux启动U盘

### 下载iso系统文件
下载哪种系统看自己喜欢，这次例子是以`linux mint`为例


### iso文件转成dmg镜像文件

```sh
~/Downloads $ hdiutil convert -format UDRW -o linuxmint.dmg linuxmint-19-cinnamon-64bit.iso
正在读取Driver Descriptor Map（DDM：0）…
正在读取Linux Mint 19 Cinnamon 64-bit   （Apple_ISO：1）…
正在读取Apple（Apple_partition_map：2）…
正在读取Linux Mint 19 Cinnamon 64-bit   （Apple_ISO：3）…
..............................................................................
正在读取EFI（Apple_HFS：4）…
..............................................................................
正在读取Linux Mint 19 Cinnamon 64-bit   （Apple_ISO：5）…
..............................................................................
已耗时： 5.026s
速度：368.9M 字节/秒
节省：0.0%
created: /Users/chenjinle/Downloads/linuxmint.dmg

```

### 把dmg写入U盘
```sh
~/Downloads $ diskutil list
~/Downloads $ diskutil umountDisk /dev/disk2
~/Downloads $ sudo dd bs=1m if=linuxmint.dmg of=/dev/rdisk2
```


### 最后
可以重启系统，用U盘引导，就可以看到Linux界面