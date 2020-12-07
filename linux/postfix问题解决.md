# postconf: warning: inet_protocols: IPv6 support is disabled: Address family not supported by protocol 问题解决

出现这个错误是因为内核不能支持IPv6。
### 解决方法
```bash
vi /etc/postfix/main.cf
# 修改inet_protocols参数
inet_protocols=ipv4
```
然后重启postfix即可
```bash
[root@sz1 /]# /etc/init.d/postfix restart
Shutting down postfix:                                     [  OK  ]
Starting postfix:                                          [  OK  ]
```

inet_protocols支持下面几种配置方式：
```bash
inet_protocols = ipv4       (只开启IPv4)
inet_protocols = all        (开启IPv4，如果系统支持IPv6也开启)
inet_protocols = ipv4, ipv6 (开启IPv4和IPv6)
inet_protocols = ipv6       (只开启IPv6)
```