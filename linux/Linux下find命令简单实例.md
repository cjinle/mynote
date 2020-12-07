# Linux下find命令简单实例

Linux `find`命令用来查找文件，
功能非常强大，也很复杂，
这里只是简单介绍几个简单参数


## 查看帮助
```
[root@localhost ~]# find --help
用法：find [路径...] [表达式]
```
1. 查找/usr路径下名为time.c的文件（包括子目录）-name 后面的字符串可用正则如： `find /usr -name "[a-z]ime.*"`
```
[root@localhost usr]# find /usr -name "time.c"
/usr/share/systemtap/runtime/time.c
/usr/local/src/subversion-1.3.2/apr/time/unix/time.c
/usr/local/src/subversion-1.3.2/apr/time/win32/time.c
/usr/local/src/subversion-1.3.2/subversion/libsvn_subr/time.c
```
2. 查找/usr目录名为share的目录，-type为查找的类型(d:目录 f:普通文件 b:块设备文件 c:字符设备文件 p:管道文件 l:符号链接文件)
```
[root@localhost usr]# find /usr -name "share" -type d
/usr/kerberos/share
/usr/share
/usr/local/share
```

3. 查找/root目录下权限为755的文件，可以组合其它参数，如：-name -type ...
```
[root@localhost usr]# find /root -perm 755
/root/cpp
/root/cpp/a.out
/root/cjinle
/root/cjinle/locks
```

4. 查找/home目录下文件属主是root用户
```
[root@localhost usr]# find /home -user root
/home
/home/swap
```

.


## 按时间范围
```sh
find *.tar.gz -ctime +90 -exec /bin/rm -f {} \;

find *.tar.gz -ctime +90 -exec /bin/rm -f {} \;

find /data/wwwroot/publish/ -name *.tar.gz -ctime +90 -exec /bin/rm -f {} \;
```

`find`命令非常强大，熟练掌握这些参数，让你在工作得心应手