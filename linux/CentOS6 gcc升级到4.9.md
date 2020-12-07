# CentOS6 gcc升级到4.9

因为centos6默认的gcc版本太低，如果要编译安装一些其它软件的时候，
会提示gcc的版本太低，但系统yum源没有提示更高版本的软件包

这个时候只能手动下载更高版本的gcc源码包进行源码安装

### 操作步骤

```
wget http://ftp.tsukuba.wide.ad.jp/software/gcc/releases/gcc-4.9.4/gcc-4.9.4.tar.gz
tar xvf gcc-4.9.4.tar.gz -C /usr/src
cd /usr/src/gcc-4.9.4/
./contrib/download_prerequisites   # 下载一些依赖库
mkdir build && cd build
../configure -enable-checking=release -enable-languages=c,c++ -disable-multilib  
make && make install

/usr/local/bin/gcc -v
```