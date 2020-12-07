# docker容器管理 (3)

## 创建容器

```
cjinle@debian:~$ sudo docker create -it ubuntu
b9ecd73aa0afc5d401a31204abf5407df47e7d2d015f831ee79b721e2c43040e
cjinle@debian:~$ sudo docker ps -l | grep b9
b9ecd73aa0af        ubuntu              "/bin/bash"         25 seconds ago      Created                                 peaceful_wozniak
```

## 新建并启动容器

```
cjinle@debian:~$ sudo docker run ubuntu /bin/echo 'hello world'
hello world
cjinle@debian:~$ sudo docker ps -l
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
e0ed90989867        ubuntu              "/bin/echo 'hello ..."   43 seconds ago      Exited (0) 43 seconds ago                       cocky_blackwell
# 创建进行终端
cjinle@debian:~$ sudo docker run -it ubuntu /bin/bash
root@3468bcdb3e61:/# 
```

## 守护态运行

```
cjinle@debian:~$ sudo docker run -d ubuntu /bin/bash -c "while true; do echo 'hello world'; sleep 1; done"
5c4e0180dd79dc6484d4d47dfeae1500184f0132e1434b721b143dabb7251a26
cjinle@debian:~$ sudo docker logs -f 5c4
hello world
hello world
hello world
hello world
hello world
```

## 停止容器

```
cjinle@debian:~$ sudo docker stop 5c4
5c4
cjinle@debian:~$ sudo docker ps -l
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS                        PORTS               NAMES
5c4e0180dd79        ubuntu              "/bin/bash -c 'whi..."   About a minute ago   Exited (137) 12 seconds ago                       quirky_galileo
```

## 进入容器

```
# attach 命令
cjinle@debian:~$ sudo docker run -idt ubuntu
e0242339397c236582bde8dfa0a06eab3693b270e9c68a5d0dacadfd03f750c5
cjinle@debian:~$ sudo docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                     NAMES
e0242339397c        ubuntu              "/bin/bash"              7 seconds ago       Up 7 seconds                                  hardcore_franklin
cjinle@debian:~$ sudo docker attach hardcore_franklin
root@e0242339397c:/#

# exec 命令
cjinle@debian:~$ sudo docker start e02
e02
cjinle@debian:~$ sudo docker ps 
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                     NAMES
e0242339397c        ubuntu              "/bin/bash"              3 minutes ago       Up 2 seconds                                  hardcore_franklin
root@e0242339397c:/# 
```

## 删除容器

```
cjinle@debian:~$ sudo docker stop e02
e02
cjinle@debian:~$ sudo docker ps -l
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
e0242339397c        ubuntu              "/bin/bash"         6 minutes ago       Exited (0) 10 seconds ago                       hardcore_franklin
cjinle@debian:~$ sudo docker rm e0242339397c
e0242339397c
```
