# 安装国内版composer

__国内版和国际版没有什么不同，只是因为国际版经常网络问题__

## 下载 Composer

安装前请务必确保已经正确安装了 PHP。打开命令行窗口并执行 `php -v` 查看是否正确输出版本号。


打开命令行并依次执行下列命令安装最新版本的 Composer：

```sh
php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"

php composer-setup.php

php -r "unlink('composer-setup.php');"
```

执行第一条命令下载下来的 `composer-setup.php` 脚本将简单地检测 `php.ini` 中的参数设置，如果某些参数未正确设置则会给出警告；然后下载最新版本的 `composer.phar` 文件到当前目录。

上述 3 条命令的作用依次是：


 - 下载安装脚本 － composer-setup.php － 到当前目录。
 - 执行安装过程。
 - 删除安装脚本。


## Mac 或 Linux 系统下安装
打开命令行窗口并执行如下命令将前面下载的 `composer.phar` 文件移动到 /usr/local/bin/ 目录下面：

```sh
sudo mv composer.phar /usr/local/bin/composer
```

_最后重新打开一个命令行窗口试一试执行 `composer --version` 看看是否正确输出版本号。_