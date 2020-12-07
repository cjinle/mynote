# Linux密码生成工具(grub-md5-crypt)



```
[root@localhost ~]# head -n 1 /etc/shadow
root:$1$EunNVfmW$c2DyNW20ur1UdDQNg2fUO0:14552:0:99999:7:::
```


__这个密码可以用Linux自带的命令grub-md5-crypt来生成__

```
#密码为123123加密后的密文
[root@localhost ~]# grub-md5-crypt
Password:
Retype password:
$1$8DTf40$DmTqozwti8NRjrnT3969B/

```

