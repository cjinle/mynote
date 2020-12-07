# centos7 /tmp的systemd-private目录问题

### PrivateTmp属性有什么好处
`/tmp`是所有用户和服务共享的目录，都有读写权限，那就存在安全性问题，所以每个服务将tmp目录隔离，能保证一定的安全性。每个服务在启动的时候创建目录，停止的时候删除目录，好处是不需要单独写定期删除临时文件的脚本了

以前centos6 php 写`/tmp`目录没有问题，现在会生成一个`systemd-private-xxx-php.service`

```
[root@localhost /]# ls /tmp
303_4.txt
303_5.txt
systemd-private-3590ed0445d948539ec508f1d31ccdd1-chronyd.service-0dCNmh
systemd-private-3590ed0445d948539ec508f1d31ccdd1-nginx.service-pB5vih
systemd-private-3590ed0445d948539ec508f1d31ccdd1-rh-mysql57-mysqld.service-hOiKPA
xxx.log
```

### 修改回写/tmp

```
systemctl edit rh-php73-php-fpm
```

**修改内容**
```
[Service]
PrivateTmp=false
```

```
systemctl restart rh-php73-php-fpm
```

*需要重启php-fpm脚本才行，reload没有生效*