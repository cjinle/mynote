# Linux下bc计算器输入输出进制切换

众所周知，Linux的终端计算器bc非常强大且好用。
今天我们就介绍一下如果在bc进行进制之间切换的。

### 一、如果用一条命令来转数字，可以用echo命令和管道结合bc。如下：

#### 10进制转2进制：
```
[root@localhost ~]# echo "obase=2;ibase=10;255" | bc
11111111
```

#### 10进制转16进制：
```
[root@localhost ~]# echo "obase=16;ibase=10;255" | bc
FF
```

#### 16进制转10进制：
```
[root@localhost ~]# echo "ibase=16;obase=2;FF" | bc
11111111
```

### 二、还可以用bc的交互模式来转换，最后Ctrl-D，或者输入quit退出。
```
[root@localhost ~]# bc
bc 1.06
Copyright 1991-1994, 1997, 1998, 2000 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
obase=2
ibase=10
255
11111111
```