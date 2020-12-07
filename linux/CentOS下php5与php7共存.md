# CentOS下php5与php7共存

## 先安装php7

安装过程略，路径在`/usr/local/php`

## 安装php5

```
// php-5.6.10
./configure --prefix=/usr/local/php5 --enable-fpm --with-config-file-path=/usr/local/php5/etc  --with-libxml-dir --with-zlib --enable-bcmath  --with-curl  --enable-ftp --with-gd --with-jpeg-dir --with-png-dir --with-freetype-dir  --enable-gd-native-ttf --enable-mbstring --with-mcrypt --with-mhash --with-mysql --with-mysqli --with-pdo-mysql --with-iconv-dir=/usr --enable-zip --enable-sockets
make ZEND_EXTRA_LIBS='-liconv'
make install
cp php.ini-production /usr/local/php5/etc/php.ini
```

## 安装phpredis

```
[root@dev phpredis-2.2.5]# /usr/local/php5/bin/phpize
[root@dev phpredis-2.2.5]# ./configure --with-php-config=/usr/local/php5/bin/php-config 
[root@dev phpredis-2.2.5]# make && make install
```

## 修改php.ini文件
```ini
# vim /usr/local/php5/etc/php.ini

# 增加下面扩展引用
extension=redis.so
```
