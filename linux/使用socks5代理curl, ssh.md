# 使用socks5代理curl, ssh


如果你本地刚好有一个socks5的代理`127.0.0.1:1080`

## curl访问网址
```sh
curl -x socks5h://127.0.0.1:1080 https://www.google.com.hk
```

## ssh登录
_前提装好nc工具，netcat-openbsd版本_
```sh
ssh root@192.168.1.102 -p 22 -o "ProxyCommand nc -X 5 -x 127.0.0.1:1080 %h %p"
```

## 终端下走代理
```sh
export http_proxy=socks5h://127.0.0.1:1080
export https_proxy=socks5h://127.0.0.1:1080
curl https://www.google.com.hk
```
