# CentOS5编译安装mongodb

mongodb有已经编译好的二进制包，解压到对应目录就可以使用。
下面介绍一下，怎么从源码进行编辑安装。

### 安装前：
**安装scons**
```bash
wget http://prdownloads.sourceforge.net/scons/scons-2.3.4.tar.gz
python setup.py install
```

### 下载mongodb源码&安装：
```bash
wget https://github.com/mongodb/mongo/archive/r2.2.7-rc0.tar.gz
tar xvf r2.2.7-rc0.tar.gz -C /usr/src 
cd /usr/src/mongo-r2.2.7-rc0
scons --prefix=/usr/local/mongo install
```

### 配置：
```bash
mkdir -p /usr/local/mongo/etc
cp /usr/src/mongo-r2.2.7-rc0/rpm/mongod.conf /usr/local/mongo/etc
```


**注：如果有需要，编辑mongod.conf配置文件，指定一下数据存放的目录等等**


如我的配置：
```bash
logpath=/var/log/mongo/mongod.log
logappend=true
fork = true
dbpath=/data0/mongodb
pidfilepath = /var/run/mongodb/mongod.pid
```

### 启动：
```bash
/usr/local/mongo/bin/mongod --config=/usr/local/mongo/etc/mongod.conf
```

### 测试连接：
```
[root@localhost ~]# /usr/local/mongo/bin/mongo
MongoDB shell version: 2.2.7-rc0
connecting to: test
> show dbs;
local	0.078125GB
mydb	0.203125GB
sina	0.453125GB
wiki_bak	0.203125GB
```
