# Linux iptables简单实例（filter, nat）

iptables 总有filter, nat, mangle, raw 四张表
这里主要讨论一下filter, nat表的用法
filter表其它包括了`INPUT`, `OUTPUT`, `FORWARD`四条链
nat表包括`PREROUTING`, `POSTROUTING`, `OUTPUT`三条链


**filter表，用来进行包过滤，假如iptables不指定-t参数的话，默认就是filter表**

```
# 服务器禁止ping
[root@rhel ~]# iptables -A INPUT -p icmp -j DROP
# 禁止192.168.113.2 ping服务器
[root@rhel ~]# iptables -A INPUT -p icmp -s 192.168.113.2 -j DROP

# 只允许192.168.113.1 IP ping 服务器
[root@rhel ~]# iptables -I INPUT -p icmp -s 192.168.113.1 -j ACCEPT
[root@rhel ~]# iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination         
ACCEPT     icmp --  192.168.113.1        anywhere            
DROP       icmp --  anywhere             anywhere            

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination  

# iptables增加规则马上生效，下面是删除或清除规则的命令
# 清空filter表所有规则
[root@rhel ~]# iptables -F
[root@rhel ~]# iptables -D INPUT -p icmp -s 192.168.113.1 -j ACCEPT
# 或者可以用序号删除
[root@rhel ~]# iptables -L --line
Chain INPUT (policy ACCEPT)
num  target     prot opt source               destination         
1    DROP       icmp --  anywhere             anywhere            

Chain FORWARD (policy ACCEPT)
num  target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
num  target     prot opt source               destination  

[root@rhel ~]# iptables -D INPUT 1
```

**PS:**
1.按顺序匹配,如果第一条匹配到了就直接执行这条规则的动作,不往下匹配其它规则.
2.如果第一条匹配不到,第二条也匹配不到,继续往下匹配直到找到匹配的规则,如果找不到匹配默认规则



```
# 禁止192.168.113.1访问80端口的WEB页面
[root@rhel ~]# iptables -A INPUT -p tcp --dport 80 -s 192.168.113.1 -j DROP

# 禁止192.168.113.0/24 这个网段访问WEB页面
[root@rhel ~]# iptables -A INPUT -p tcp --dport 80 -s 192.168.113.0/24 -j DROP

# 禁止192.168.113.1 SSH登录服务器
[root@rhel ~]# iptables -A INPUT -p tcp --dport 22 -s 192.168.113.1 -j DROP

# 禁止192.168.113.0/24 SSH登录服务器
[root@rhel ~]# iptables -A INPUT -p tcp --dport 22 -s 192.168.113.0/24 -j DROP
```


**nat表，一般用作路由功能**

要Linux有路由功能，要打开`ip_forward`开关
```
[root@rhel ~]# sysctl -a | grep ip_forward
net.ipv4.ip_forward = 0
# 打开路由功能
[root@rhel ~]# echo 1 > /proc/sys  
[root@rhel ~]# sysctl -a | grep ip_forward
net.ipv4.ip_forward = 1

# 上面只是临时生效，重启刚失效了，下面命令可以永久生效
[root@rhel ~]# sysctl -p
net.ipv4.ip_forward = 0
net.ipv4.conf.default.rp_filter = 1
net.ipv4.conf.default.accept_source_route = 0
kernel.sysrq = 0
kernel.core_uses_pid = 1
net.ipv4.tcp_syncookies = 1
kernel.msgmnb = 65536
kernel.msgmax = 65536
kernel.shmmax = 4294967295
kernel.shmall = 268435456
```

要有路由功能，服务器必需2块网卡

```
# SNAT:
[root@rhel ~]# iptables -t nat -A POSTROUTING -o eth1 -s 192.168.1.0/24 -j SNAT --to 192.168.20.11
[root@rhel ~]# iptables -t nat -A POSTROUTING -o eth1 -s 192.168.1.0/24 -j MASQUERARD


# DNAT:
[root@rhel ~]# iptables -t nat -A PREROUTING -i eth1 -d 192.168.20.11 -p tcp --dport 80 -j DNAT --to 192.168.1.254:80
```