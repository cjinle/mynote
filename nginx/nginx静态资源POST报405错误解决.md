# nginx静态资源POST报405错误解决

为了学习B-jui前端框架，下载了他们的源码进行DEMO测试
但里面数据都是静态json文件返回的，导致报了405错误
在网上找了一些方法，好像都没有管用，可能是因为之前的方法太过古老，
后来自己想了一个方法解决了，因为这个错误是POST导致的，用GET就没有问题
所以只要是post请求json文件，重定向用get请求就行


### 解决方法
```config
server {
	...
    location ~ .*\.json$ {
        if ($request_method ~* "POST") {
            rewrite .* http://$host$request_uri;
        }
    }
	...
}
```