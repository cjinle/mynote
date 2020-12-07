# lsof命令简单查看端口与进程

### 查看当前TCP监控的端口
```
[root@dev ~]# lsof -nP -iTCP -sTCP:LISTEN
COMMAND    PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
rpcbind   1102     rpc    8u  IPv4   8698      0t0  TCP *:111 (LISTEN)
rpcbind   1102     rpc   11u  IPv6   8701      0t0  TCP *:111 (LISTEN)
rpc.statd 1124 rpcuser    9u  IPv4   8786      0t0  TCP *:58399 (LISTEN)
rpc.statd 1124 rpcuser   11u  IPv6   8792      0t0  TCP *:46907 (LISTEN)
sshd      1244    root    3u  IPv4   9023      0t0  TCP *:22 (LISTEN)
sshd      1244    root    4u  IPv6   9027      0t0  TCP *:22 (LISTEN)
master    1323    root   12u  IPv4   9233      0t0  TCP 127.0.0.1:25 (LISTEN)
master    1323    root   13u  IPv6   9234      0t0  TCP [::1]:25 (LISTEN)
php-fpm   1375    root    7u  IPv4   9437      0t0  TCP 127.0.0.1:9000 (LISTEN)
php-fpm   1395     www    0u  IPv4   9437      0t0  TCP 127.0.0.1:9000 (LISTEN)
php-fpm   1396     www    0u  IPv4   9437      0t0  TCP 127.0.0.1:9000 (LISTEN)
nginx     1455    root   29u  IPv4   9496      0t0  TCP *:80 (LISTEN)
nginx     1455    root   30u  IPv4   9497      0t0  TCP *:8888 (LISTEN)
nginx     1458     www   29u  IPv4   9496      0t0  TCP *:80 (LISTEN)
nginx     1458     www   30u  IPv4   9497      0t0  TCP *:8888 (LISTEN)
aria2c    1494    root    5u  IPv4   9539      0t0  TCP *:6800 (LISTEN)
mysqld    1546   mysql   30u  IPv4   9648      0t0  TCP 127.0.0.1:3306 (LISTEN)
```

### 查看当前UDP端口
```
[root@dev ~]# lsof -nP -iUDP
COMMAND    PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
dhclient   943    root    5u  IPv4   8326      0t0  UDP *:68 
rpcbind   1102     rpc    6u  IPv4   8696      0t0  UDP *:111 
rpcbind   1102     rpc    7u  IPv4   8697      0t0  UDP *:853 
rpcbind   1102     rpc    9u  IPv6   8699      0t0  UDP *:111 
rpcbind   1102     rpc   10u  IPv6   8700      0t0  UDP *:853 
rpc.statd 1124 rpcuser    5r  IPv4   8778      0t0  UDP 127.0.0.1:876 
rpc.statd 1124 rpcuser    8u  IPv4   8783      0t0  UDP *:33161 
rpc.statd 1124 rpcuser   10u  IPv6   8789      0t0  UDP *:56899 
```


### 查看进程打开的文件情况
```
[root@dev ~]# lsof -p 1244
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF    NODE NAME
sshd    1244 root  cwd    DIR  253,0     4096       2 /
sshd    1244 root  rtd    DIR  253,0     4096       2 /
...
sshd    1244 root    0u   CHR    1,3      0t0    3839 /dev/null
sshd    1244 root    1u   CHR    1,3      0t0    3839 /dev/null
sshd    1244 root    2u   CHR    1,3      0t0    3839 /dev/null
sshd    1244 root    3u  IPv4   9023      0t0     TCP *:ssh (LISTEN)
sshd    1244 root    4u  IPv6   9027      0t0     TCP *:ssh (LISTEN)
```

### 查看端口情况
```
[root@dev ~]# lsof -i:9000
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
php-fpm 1375 root    7u  IPv4   9437      0t0  TCP localhost:cslistener (LISTEN)
php-fpm 1395  www    0u  IPv4   9437      0t0  TCP localhost:cslistener (LISTEN)
php-fpm 1396  www    0u  IPv4   9437      0t0  TCP localhost:cslistener (LISTEN)
```