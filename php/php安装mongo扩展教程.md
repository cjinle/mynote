# php安装mongo扩展教程

mongo db是个好东西，越来越多的项目中有使用到。
下面介绍如何安装mongo扩展

### 环境

 - nginx/1.4.4
 - PHP 5.4.22
 - MongoDB 2.4.10


### 下载扩展安装包
```
wget http://pecl.php.net/get/mongo-1.4.5.tgz
```

### 编译安装
```
tar xvf mongo-1.4.5.tgz -C /usr/src
cd /usr/src/mongo-1.4.5/
phpize
./configure --with-php-config=/usr/local/php/bin/php-config
make && make install
```

### 配置php.ini，增加下面两行
```
[mongo]
extension = /usr/local/php/lib/php/extensions/no-debug-non-zts-20100525/mongo.so
```

### 重新加载php-fpm, nginx
```
pkill php-fpm
/usr/local/php/sbin/php-fpm
/usr/local/nginx/sbin/nginx -s reload
```

### 验证是否安装成功
```
php -m | grep mongo
# 或者查看phpinfo页面
```