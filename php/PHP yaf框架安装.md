# PHP yaf框架安装

### 下载源码包
在github上下载源码包，https://github.com/laruence/php-yaf
如：wget https://github.com/laruence/php-yaf/archive/master.zip

### 编译安装
```bash
unzip yaf.zip  -d /usr/src/yaf/
phpize
./configure --with-php-config=/usr/local/php/bin/php-config
make && make install
```

### 引用库文件，重启php-fpm
在`php.ini`中引有库文件，如下：
```config
[yaf]
extension = /usr/local/php/lib/php/extensions/no-debug-non-zts-20100525/yaf.so
```
