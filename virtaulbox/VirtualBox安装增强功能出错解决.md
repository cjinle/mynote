# VirtualBox安装增强功能出错解决

**出错日志如下：**
```
Verifying archive integrity... All good.
Uncompressing VirtualBox 4.3.6 Guest Additions for Linux............
VirtualBox Guest Additions installer
Removing installed version 4.3.6 of VirtualBox Guest Additions...
Copying additional installer modules ...
Installing additional modules ...
Removing existing VirtualBox non-DKMS kernel modules       [  OK  ]
Building the VirtualBox Guest Additions kernel modules
The headers for the current running kernel were not found. If the following
module compilation fails then this could be the reason.
The missing package can be probably installed with
yum install kernel-devel-2.6.32-573.el6.i686

Building the main Guest Additions module                   [FAILED]
(Look at /var/log/vboxadd-install.log to find out what went wrong)
Doing non-kernel setup of the Guest Additions              [  OK  ]
Installing the Window System drivers                       [FAILED]
(Could not find the X.Org or XFree86 Window System.)
```
**解决方法：**
```bash
yum install kernel-headers kernel-devel
```

**小提示：**
安装相关依赖库：`yum install bzip2 gcc make kernel-devel`
安装增强工具过程：
然后手动挂载光盘
```bash
mount /dev/cdrom /mnt
/mnt/VBoxLinuxAdditions.run
```
碰到错误，查看错误日志，一般会指出安装系统所缺少的工具或库
然后再`yum search`搜索库并安装之

