# 构建docker go应用镜像

## 拉取镜像

```sh
sudo docker pull golang:1.15.5-alpine
```

## 编写Dockerfile
```Dockerfile
FROM golang:1.15.5-alpine AS build
WORKDIR /go/src/github.com/cjinle/test/main
ADD . .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo .
CMD ["./main"]
```

## 构建镜像
```sh
cd github.com/cjinle/test/main/
sudo docker build -t chenjinle/main .
```

## 测试镜像
```sh
sudo docker run --rm -it chenjinle/main
```


## 构建已经编译好的程序

### Dockerfile
```Dockerfile
FROM scratch
WORKDIR $GOPATH/src/github.com/cjinle/test/json
COPY . $GOPATH/src/github.com/cjinle/test/json
CMD ["./main"]
# CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .
```

### 编译、测试

```sh
CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .  # 生成程序
sudo docker build -t chenjinle/gojson . # 编译镜像
sudo docker run --rm -it chenjinle/gojson  # 测试
```
