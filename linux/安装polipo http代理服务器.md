# 安装polipo http代理服务器

## 安装polipo
```sh
sudo apt-get install polipo

sudo vim /etc/polipo/config
```

## 配置polipo

/etc/polipo/config
```ini
logSyslog = true
logFile = /var/log/polipo/polipo.log

socksParentProxy = "192.168.100.114:1080"
socksProxyType = socks5
logLevel = 99
```

## 重启polipo
```sh
sudo systemctl status polipo
sudo systemctl restart polipo
```

## 配置终端走代理
```sh
export https_proxy=http://127.0.0.1:8123
export http_proxy=http://127.0.0.1:8123
```