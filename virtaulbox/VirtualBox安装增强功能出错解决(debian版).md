# VirtualBox安装增强功能出错解决(debian版)

### 错误信息 /var/log/vboxadd-install.log
```
/tmp/vbox.0/Makefile.include.header:112: *** Error: unable to find the sources of your current Linux kernel. Specify KERN_DIR=<directory> and run Make again.  Stop.
Creating user for the Guest Additions.
Creating udev rule for the Guest Additions kernel module.
cjinle@debian:/mnt$ sudo apt-get install kernel-headers kernel-devel
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package kernel-headers
E: Unable to locate package kernel-devel
```

### 解决方法
```bash
cjinle@debian:/mnt$ sudo apt-get install linux-headers-$(uname -r)
```