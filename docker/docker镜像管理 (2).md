# docker镜像管理 (2)

## 获取镜像

```
cjinle@debian:~$ sudo docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
ae79f2514705: Pull complete 
5ad56d5fc149: Pull complete 
170e558760e8: Pull complete 
395460e233f5: Pull complete 
6f01dc62e444: Pull complete 
Digest: sha256:506e2d5852de1d7c90d538c5332bd3cc33b9cbd26f6ca653875899c505c82687
Status: Downloaded newer image for ubuntu:latest
```


## 查看镜像

```
cjinle@debian:~$ sudo docker images
REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
test/centos               1.0                 a7c98122fb82        39 hours ago        197MB
chenjinle/get-started     part4               548b899d7563        4 days ago          150MB
friendlyhello             latest              548b899d7563        4 days ago          150MB
chenjinle/friendlyhello   part3               3714d0476553        4 days ago          150MB
chenjinle/get-started     part3               3714d0476553        4 days ago          150MB
alpine                    latest              37eec16f1872        6 days ago          3.97MB
python                    2.7-slim            e9adbdab327d        8 days ago          138MB
ubuntu                    latest              747cb2d60bbe        3 weeks ago         122MB
redis                     latest              1fb7b6c8c0d0        3 weeks ago         107MB
centos                    latest              196e0ce0c9fb        6 weeks ago         197MB
hello-world               latest              05a3bd381fc2        7 weeks ago         1.84kB
training/webapp           latest              6fae60ef3446        2 years ago         349MB
```

## 删除镜像

```
cjinle@debian:~$ sudo docker rmi ubuntu
Untagged: ubuntu:latest
Untagged: ubuntu@sha256:506e2d5852de1d7c90d538c5332bd3cc33b9cbd26f6ca653875899c505c82687
Deleted: sha256:747cb2d60bbecbda48aff14a8be5c8b913ca69318a6067e57c697f8a78dda06e
Deleted: sha256:ec1fd849ff0a8f0aa2fd1acc29ad5dabbc79b89f63b74a4f54e31a7b0a100aa1
Deleted: sha256:e3f6dffa20cf36460d23bfb22e17be6e5339891f8537f32db79887caf832048b
Deleted: sha256:c213ffdc9f7032702de5a8e9045fcce2353b7221ef6bf4509e02005cfc858f58
Deleted: sha256:3fddf55a451aa43707518f2d8788c12ee5eb1f1e3075433f5bcf4d445d5c275d
Deleted: sha256:0f5ff0cf6a1c53f94b15f03536c490040f233bc455f1232f54cc8eb344a3a368
```

## 其它
如果在创建容器的指定对于的源镜像时，如果本地没有，则会直接到线上下载对应的镜像