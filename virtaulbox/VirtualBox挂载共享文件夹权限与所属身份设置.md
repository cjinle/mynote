# VirtualBox挂载共享文件夹权限与所属身份设置

VirtualBox共享文件夹功能很好用，可以做到虚拟机与母机之间的文件共享
但默认挂载的权限与所属身份和我们所需要的情况不符合，下面可以设置指定的挂载方式

### 在/etc/rc.local加上
```bash
mount -o umask=002,gid=www,uid=www -t vboxsf wwwroot /media/sf_wwwroot
```
