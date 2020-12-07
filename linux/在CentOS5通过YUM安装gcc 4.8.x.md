# 在CentOS5通过YUM安装gcc 4.8.x

`centos5/redhat5` 自带的GCC已经很低了，一般是4.1左右，但如果安装一些软件需求高版本的gcc就比较麻烦了。

除了下源码编译安装外，这里介绍通过YUM源来直接安装

```
wget http://people.centos.org/tru/devtools-2/devtools-2.repo -O /etc/yum.repos.d/devtools-2.repo
yum install devtoolset-2-gcc devtoolset-2-binutils devtoolset-2-gcc-c++
ln -s /opt/rh/devtoolset-2/root/usr/bin/* /usr/local/bin/
hash -r
gcc --version
```

大功告成！
