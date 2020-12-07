# debian9自启动rc.local配置

debian9下默认是没有`rc.local`文件了，但服务却是有的，默认是关闭状态
要想开启，需要下面几个步骤：

## 1. 新建rc.local文件
```sh
#!/bin/sh -e

echo rc.local

exit 0
```

## 2. 启动rc.local服务
```sh
sudo systemctl start rc.local
```