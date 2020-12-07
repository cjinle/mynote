# 解决sudo执行命令很慢的问题

1. 首先先确定自己是否有/etc/sudoers里面
2. 绑定主机名
```
[root@bogon etc]# hostname
bogon
[root@bogon etc]# vim /etc/hosts
```

增加一行，把自己的主机增加进去
如下面所示
```
# Do not remove the following line, or various programs
# that require network functionality will fail.
127.0.0.1               localhost.localdomain localhost
::1             localhost6.localdomain6 localhost6
192.168.163.131 bogon
```
