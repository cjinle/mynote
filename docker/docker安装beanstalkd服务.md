# docker安装beanstalkd服务

因最近要使用队列服务，决定选择比较轻量的`beanstalk`

## 安装启动
```
// 拉取镜像
$ sudo docker pull bevand10/alpine-beanstalk
// 启动
$ sudo docker run --name beanstalk -p 11300:11300 -d bevand10/alpine-beanstalk
// 查看启动情况
$ sudo docker ps | grep beans
c9e7acec11ae        bevand10/alpine-beanstalk   "/run.sh"                5 days ago          Up 5 days           0.0.0.0:11300->11300/tcp   beanstalk
// 重启
$ sudo docker restart c9e7acec11ae
c9e7acec11ae
```

## 启动并绑定目录
```
sudo docker run --name beanstalk2 -p 11301:11300 -v /data/baeanstore:/binlog -d bevand10/alpine-beanstalk
```