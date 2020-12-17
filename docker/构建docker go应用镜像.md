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