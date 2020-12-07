# Linux网络配置（CentOS为例）

网络配置，首先先看下你的网线有没有接好，
不要觉得好笑，可以好多原因就是因为网线没接好。

可以用运行命令`mii-tool`查看一下，正常的话会显示link OK
__PS:VM虚拟机下不支持__


 - ping 127.0.0.1看网卡驱动是否安装正常
 - ifconfig 查看以太网卡的信息，因为可以看到很多信息，一般是eth0, 
   没有启动的话，就/etc/init.d/network start
   如：
```
   eth0      Link encap:Ethernet  HWaddr 00:0C:29:54:B4:99
          inet addr:192.168.113.133  Bcast:192.168.113.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:3140 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1231 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:1764092 (1.6 MiB)  TX bytes:80116 (78.2 KiB)
          Interrupt:67 Base address:0x2024
          
```
 - 如果你的没有IP，或者上不去网络，请看下面步骤：


## 临时配置IP
 - dclicent eth0   #这个是自动让DHCP服务器分配IP
 -  如果上面的不行，你可以临时为自己分配IP
   ifconfig eth0 addr 192.168.113.134 netmask 255.255.255.0
   /etc/init.d/network restart #配置完，要记得重启网络
   

## 手动配置静态IP
打开`/etc/sysconfig/network-script/ifcfg-eth0`
__PS:centos, redhat等版本的Linux是这个，其它的有所不同__

然后按实际输入你的IP信息

```ini
DEVICE=eth0
BOOTPROTO=static
IPADDR=192.168.113.134
NETMASK=255.255.255.0
GATEWAY=192.168.113.1
HWADDR=00:19:e0:00:94:2a
ONBOOT=yes
```
_PS:HWADDR是网卡MAC地址，上面默认就有的，不用修改_
主要配置好`IPADDR`, `NETMASK`, `GATEWAY`, `BOOTPROTO`就好