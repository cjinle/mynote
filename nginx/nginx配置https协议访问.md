# nginx配置https协议访问

## 准备ssl证书

免费域名证书申请： __Let’s Encrypt泛域名免费ssl证书__


## 配置nginx

### http和https兼容访问

```sh
server {
	listen 80;
	listen 443 ssl;
	root /data/wwwroot/;
	index index.php index.html;
	server_name xxx.com www.xxx.com;

	ssl_certificate cert/xxx.pem;   # nginx配置的cert目录下，如果没有，那就写完整路径吧
	ssl_certificate_key cert/xxx.key;
	ssl_session_timeout 5m;
	ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
	ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
	ssl_prefer_server_ciphers on;
	...
}
```

### 只允许https访问，http访问跳转到https
```sh
server {
	listen 80;
        server_name xxx.com www.xxx.com;
	rewrite ^(.*)$ https://www.xxx.com$1 permanent;
}
server {
	listen 443 ssl;
	root /data/wwwroot/;
	index index.php index.html;
	server_name xxx.com www.xxx.com;

	ssl on;
	ssl_certificate cert/xxx.pem;   # nginx配置的cert目录下，如果没有，那就写完整路径吧
	ssl_certificate_key cert/xxx.key;
	ssl_session_timeout 5m;
	ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
	ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
	ssl_prefer_server_ciphers on;
	...
}
```

然后`reload nginx`测试就OK了。