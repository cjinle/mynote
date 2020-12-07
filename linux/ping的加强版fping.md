# ping的加强版fping

刚发现一个ping的加强版本--fping，非常好用
fping不是系统命令，你需要另外安装

## Linux:
```
[root@bogon ~]#wget http://fping.sourceforge.net/download/fping.tar.gz
[root@bogon ~]#tar xvzf fping.tar.gz
[root@bogon ~]#cd fping-2.4b.2_to
[root@bogon fping-2.4b2_to]#./configure
[root@bogon fping-2.4b2_to]#make && make install
```

这样就安装完成了

使用：
```
[root@bogon fping-2.4b2_to]# fping -t 100 -g 192.168.18.1 192.168.18.10         
192.168.18.1 is alive
192.168.18.3 is alive
192.168.18.4 is alive
192.168.18.7 is alive
192.168.18.8 is alive
192.168.18.9 is alive
192.168.18.10 is alive
192.168.18.2 is unreachable
192.168.18.5 is unreachable
192.168.18.6 is unreachable
```

`fping`也有windows版本的，安装使用都很简单
这样就是不作详述了


