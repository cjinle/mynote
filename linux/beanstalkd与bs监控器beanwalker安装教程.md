# beanstalkd与bs监控器beanwalker安装教程

### beanstalkd安装

[下载源码包](https://github.com/kr/beanstalkd/archive/v1.10.tar.gz)

### 编译安装
```bash
tar xvf beanstalkd-1.10.tar.gz -C /usr/src
cd /usr/src/beanstalkd-1.10
make && make install
```

### 启动
```bash
[root@dev beanstalkd-1.10]# beanstalkd &
[root@dev beanstalkd-1.10]# ps -ef | grep beanstalkd
root      3547  1757  0 10:22 pts/1    00:00:00 beanstalkd
root      3611  3552  0 10:55 pts/0    00:00:00 grep beanstalkd
```

### beanwalker安装
因为这个工具是go语言写的，如果要编译安装则需要安装golang
但也可以直接下载已经编译好的二进制bin文件

### 下载启动
```bash
wget https://github.com/kadekcipta/beanwalker/releases/download/v0.0.2/beanwalker_v0.0.2_linux_amd64.tar.bz2

tar xvf beanwalker_v0.0.2_linux_amd64.tar.bz2
mv beanwalker /usr/local/bin

beanwalker  # 启动

```
