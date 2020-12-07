# VirtualBox下debian虚拟机加第二块网卡并启动

### 操作步骤


 - virtualbox管理下在对应的虚拟机下，设置-网络-网卡2-启用就可
 - 在debian虚拟机下配置网卡并启动


### 添加网卡
![vmbox3](uploads/2017/10/vmbox3.png)

### debian配置网卡

#### 查看新添加的网卡的名称
```bash
root@debian:~# ls /sys/class/net 
docker0  enp0s3  enp0s8  lo
```

#### 配置启动脚本
```bash
root@debian:~# vim /etc/network/interfaces
```

在文件后面追加

```bash
# 第二块网卡启动
allow-hotplug enp0s8
iface enp0s8 inet dhcp
```

#### 启动网卡
```bash
root@debian:~# ifup enp0s8
Internet Systems Consortium DHCP Client 4.3.5
Copyright 2004-2016 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/

Listening on LPF/enp0s8/08:00:27:cd:90:c9
Sending on   LPF/enp0s8/08:00:27:cd:90:c9
Sending on   Socket/fallback
DHCPDISCOVER on enp0s8 to 255.255.255.255 port 67 interval 8
DHCPDISCOVER on enp0s8 to 255.255.255.255 port 67 interval 13
DHCPREQUEST of 192.168.1.129 on enp0s8 to 255.255.255.255 port 67
DHCPOFFER of 192.168.1.129 from 192.168.1.251
DHCPACK of 192.168.1.129 from 192.168.1.251
bound to 192.168.1.129 -- renewal in 619498 seconds.
```

#### 查看网卡信息
```bash
root@debian:~# ifconfig enp0s8
enp0s8: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.129  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::a00:27ff:fecd:90c9  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:cd:90:c9  txqueuelen 1000  (Ethernet)
        RX packets 3171  bytes 220474 (215.3 KiB)
        RX errors 0  dropped 159  overruns 0  frame 0
        TX packets 12  bytes 1472 (1.4 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```
