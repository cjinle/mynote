# 隐藏nginx的版本号

**vim /usr/local/nginx/conf/nginx.conf**
在http作用域加上`server_tokens off;`
```config
http {
#...
	server_tokens off;
#...
}
```

**vim /usr/local/nginx/conf/fcgi.conf**
把`/$nginx_version`去掉
```bash
#fastcgi_param  SERVER_SOFTWARE    nginx/$nginx_version;
fastcgi_param  SERVER_SOFTWARE    nginx;	
```


**然后重载nginx**
```bash
/usr/local/nginx/sbin/nginx -s reload
```


