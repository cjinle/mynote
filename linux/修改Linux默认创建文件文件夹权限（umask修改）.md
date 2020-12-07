# 修改Linux默认创建文件文件夹权限（umask修改）

Linux下，一般创建文件或者文件夹都有一个默认的权限
这个数值是靠Linux的`umask`值决定的。
而默认的root用户和普通用户的umask也不同
```
root:022
普通用户：002
```

所以导致root创建和普通用户的创建的权限不同

```
root: 
-------
文件：644    // 666-022=644
-rw-r--r-- 1 root root    0 09-03 19:03 testfile
文件夹：755  // 777-022=755
drwxr-xr-x 2 root root 4.0K 09-03 19:02 testdir

普通用户：
--------
文件：664   // 666-002=664
-rw-rw-r-- 1 test test 0 09-03 19:05 testfile
文件夹：775  // 777-002=775
drwxrwxr-x 2 test test 4.0K 09-03 19:06 testdir
```

## 修改umask值

临时修改（只是当前终端有效，下次登录就没有了）
`umask 000` 
__注：000为权限所表示的八进制数据，如：022, 002__


__永久修改：__
修改`/etc/bashrc` 文件

行8~行12
```sh
if [ $UID -gt 99 ] && [ "`id -gn`" = "`id -un`" ]; then
    umask 002 
else
    umask 022 
fi
```

 - 第一个为普通用户的`umask`,
 - 第二个为`root`用户的

然后重要加载，或重新登录就可以了

