# docker安装mysql5.6

## 下载镜像
```
cjinle@debian:~$ sudo docker pull mysql:5.6
```

## 启动mysql

```
cjinle@debian:~$ sudo docker run --name mysql5.6 -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.6
80b766cca7ce0af73787a626153a92286cc7ab8c125e42c1c75e3e680ecefcf5
```

## 查看进程

```
cjinle@debian:~$ sudo docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
80b766cca7ce        mysql:5.6           "docker-entrypoint..."   8 minutes ago       Up 8 minutes        0.0.0.0:3306->3306/tcp   mysql5.6
d4d5aa2e10f7        redis               "docker-entrypoint..."   3 hours ago         Up 3 hours          0.0.0.0:6379->6379/tcp   musing_wescoff
```

## 连接测试
_用有mysql客户端的登录测试_
```
[root@dev ~]# mysql -uroot -p123456 -h192.168.56.101
Warning: Using a password on the command line interface can be insecure.
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 20
Server version: 5.6.38 MySQL Community Server (GPL)

Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```