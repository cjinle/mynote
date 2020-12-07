# mount wrong fs type, bad option, bad superblock错误解决

新安装的debian上，想挂载nfs分区，发现报了以下的错误

```bash
cjinle@debian:/sbin$ sudo /bin/mount -t nfs -o hard 192.168.1.129:/nfs /data
mount: wrong fs type, bad option, bad superblock on 192.168.1.129:/nfs,
       missing codepage or helper program, or other error
       (for several filesystems (e.g. nfs, cifs) you might
       need a /sbin/mount.<type> helper program)

       In some cases useful info is found in syslog - try
       dmesg | tail or so.
```

### 解决方法
```bash
cjinle@debian:/sbin$ sudo apt-get install nfs-common -y
cjinle@debian:/sbin$ sudo service portmap status
```