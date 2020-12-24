# 搭建docker私有仓库


## 搭建环境

```sh
sudo docker run -d -p 5000:5000 --restart always --name registry registry:2

sudo docker image tag chenjinle/gojson:0.0.1-beta localhost:5000/gojson:0.0.1-beta

sudo docker push localhost:5000/gojson:0.0.1-beta

```

## 测试
```
http://192.168.56.101:5000/v2/_catalog
{"repositories":["gojson"]}
```



