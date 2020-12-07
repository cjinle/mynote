# 64位ubuntu10.04安装 KVM

### 1.检测自己的电脑是否支持安装KVM
`egrep -c '(vmx|svm)' /proc/cpuinfo`

哪里结果为0的话，很不幸告诉你，
因为你的CPU不支持虚拟化，所以装不了`KVM`
结果大于1的话，就有可能装

### 2.你的系统是64位的系统

### 3.安装需要的软件包
```
$ sudo apt-get install qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils virt-manger
```

### 4.把当前用户加到libvirtd, kvm组下
```
$ sudo adduser `id -un` libvirtd
$ sudo adduser `id -un` kvm
```
然后重新登录，不出意外的话，就可以正常使用`KVM`了。



