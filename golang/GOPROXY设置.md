# GOPROXY设置



在`Go 1.13`中，我们可以通过GOPROXY来控制代理，以及通过GOPRIVATE控制私有库不走代理。

## 设置GOPROXY代理
```
go env -w GOPROXY=https://goproxy.cn,direct
```

## 设置GOPRIVATE来跳过私有库

比如常用的Gitlab或Gitee，中间使用逗号分隔
```
go env -w GOPRIVATE=*.gitlab.com,*.gitee.com
```

## 常见异常
如果在运行go mod vendor时，提示Get https://sum.golang.org/lookup/xxxxxx: dial tcp 216.58.200.49:443: i/o timeout，则是因为Go 1.13设置了默认的GOSUMDB=sum.golang.org，这个网站是被墙了的，用于验证包的有效性，可以通过如下命令关闭：

```
go env -w GOSUMDB=off
```

## 私有仓库自动忽略验证
可以设置 GOSUMDB="sum.golang.google.cn"， 这个是专门为国内提供的sum 验证服务。
```
go env -w GOSUMDB="sum.golang.google.cn"
```

w 标记 要求一个或多个形式为 NAME=VALUE 的参数， 并且覆盖默认的设置
