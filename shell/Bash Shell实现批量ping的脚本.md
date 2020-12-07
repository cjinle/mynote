# Bash Shell实现批量ping的脚本

思路是通过循环，去`ping`主机地址
用`$?`来判断上次命令是否成功得出主机是否存在

代码如下：

```sh
#!/bin/bash

for i in `seq 10`
do
    ip=192.168.113.$i
    ping -c 2 $ip > /dev/null 2>&1
    [ $? -eq 0 ] && echo "$ip is alive"  || echo "$ip is not alive"
done
```


结果：
```
[root@localhost shell]# sh 3.sh
192.168.113.1 is not alive
192.168.113.2 is alive
192.168.113.3 is not alive
192.168.113.4 is not alive
192.168.113.5 is not alive
192.168.113.6 is not alive
192.168.113.7 is not alive
192.168.113.8 is not alive
192.168.113.9 is not alive
192.168.113.10 is not alive
```

之前有写过，有一个叫`fping`工具的。

