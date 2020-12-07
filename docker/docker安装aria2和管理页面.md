# docker安装aria2和管理页面

## 拉源
```sh
sudo docker pull xujinkai/aria2-with-webui
```


## 启动
```sh
sudo docker run -d \
--name aria2-with-webui \
-p 6800:6800 \
-p 6880:80 \
-p 6888:8080 \
-v /data/wwwroot/downloads:/data \
-v /usr/local/etc:/conf \
-e SECRET= \
xujinkai/aria2-with-webui

```