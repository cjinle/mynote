# nginx client intended to send too large body错误解决

最近在搞文件上传的东西，但碰到了一个问题，就是上传的文件如果稍微有点大的时候，
就报了这样的错误：

```
2018/05/02 08:15:45 [error] 11091#11091: *4261 client intended to send too large body: 5251073 bytes, client: xx.xx.xx.xx, server: xx.xx.xx.xx, request: "POST /index.php HTTP/1.1", host: "xx.xx.xx.xx:8081"
```

这是nginx的`client_max_body_size`默认是`1m`，如果超过这个值，就会报上面的错误了。

## 解决方法
修改nginx的配置，在server配置块指定大小，如果要不限制，则把此值设置为0则可。

```
server {
	...
	client_max_body_size 32m;
	...
}
```