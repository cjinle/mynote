# nginx日志分析工具goaccess安装使用

## 测试环境
nginx日志是centos6下yum安装的，分析工具安装在debian9系统上

## 安装
```sh
sudo apt-get install goaccess
```

## 配置
```
sudo vim /etc/goaccess.conf
```

这个可以按实际日志格式进行配置，如下面nginx日志格式如下：

```
{
	log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
}
```

则对应的配置是：

```sh
time-format %T
date-format %d/%b/%Y
log-format %h - %^ - [%d:%t %^] "%r" %s %b "%R" "%u"
```

更新参数说明 [https://goaccess.io/man](https://goaccess.io/man)


## 日志分析
```sh
goaccess -f access.log-20190318 -c -a > access.out.html
```

然后用浏览器打开`access.out.html`文件即可