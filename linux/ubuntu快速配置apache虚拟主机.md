# ubuntu快速配置apache虚拟主机

在ubuntu下，用`apt-get install`安装的apache，配置虚拟主机和平常在其它平台的不大一样
如果我想快速在本地建一个test.com的虚拟主机
下面是操作步骤：

### 1. 先绑定test.com到127.0.0.1
```
#vim /etc/hosts
# 加上
127.0.0.1 test.com
```

### 2. 配置虚拟主机文件
```
#cd /etc/apache2/sites-available
#vim test
# 加上
<VirtualHost *:80>
	ServerName test.com
	DocumentRoot /home/lok/workspace/PhpTest
	ErrorLog ${APACHE_LOG_DIR}/test_access.log
	CustomLog ${APACHE_LOG_DIR}/test_access.log common
</VirtualHost>
```

### 3. 启用test.com
```
#a2ensite test
```

### 4. 重启apache2
```
#service apache2 restart
```

这样就算完成了。



**备注：**
重启apache2有可以会出现下面的告警
`"apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1 for ServerName"`

解决方法：在httpd.conf加上 `ServerName localhost:80` 就行。
