# nginx反向代理配置

### vhost配置
```config
server {
  listen 80;
  server_name xx1.pouman.com;
  location / {
    proxy_pass http://xx2.pouman.com;
    proxy_set_header Host 127.0.0.1:80;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Via "nginx";
  }
}
```

