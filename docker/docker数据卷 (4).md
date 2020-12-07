# docker数据卷 (4)

## 在容器内创建一个数据卷

```
cjinle@debian:~$ sudo docker run -d -P --name web -v /webapp training/webapp python app.py
16664c427814b34d13691af84a84c2c3613b1d463b0e1987b56ded742148d1a0
cjinle@debian:~$ sudo docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                     NAMES
16664c427814        training/webapp     "python app.py"          9 minutes ago       Up 9 minutes        0.0.0.0:32770->5000/tcp   web
1985f0548dc0        redis               "docker-entrypoint..."   2 days ago          Up 2 days           0.0.0.0:6379->6379/tcp    jolly_lovelace
cjinle@debian:~$ sudo docker exec -ti 16664c427814 /bin/bash
root@16664c427814:/opt/webapp# ls
Procfile  app.py  requirements.txt  tests.py
root@16664c427814:/opt/webapp# cd /webapp
```

## 挂载一个主机目录作为数据卷

```
cjinle@debian:~$ sudo docker run -d -P --name  web -v /src/webapp:/opt/webapp training/webapp python app.py
# 只读
cjinle@debian:~$ sudo docker run -d -P --name  web -v /src/webapp:/opt/webapp:ro training/webapp python app.py
```

## 挂载一个主机文件作为数据卷

```
cjinle@debian:~$ sudo docker run --rm -it -v ~/.bash_history:/.bash_history ubuntu /bin/bash
root@8678d2cc597e:/#
```


## 数据卷容器

```
cjinle@debian:~$ sudo docker run -it -v /dbdata --name dbdata ubuntu
root@c8dca94a15dd:/# cd /dbdata/
root@c8dca94a15dd:/dbdata# ls
aa 

cjinle@debian:~$ sudo docker run -it --volumes-from dbdata --name db1 ubuntu
root@c8dca94a15dd:/# ls
bin  boot  dbdata  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@c8dca94a15dd:/# cd /dbdata/
root@c8dca94a15dd:/dbdata# ls
aa
root@c8dca94a15dd:/dbdata# cat aa 
123
root@c8dca94a15dd:/dbdata# ls
aa
root@c8dca94a15dd:/dbdata# echo 222 >> aa

cjinle@debian:~$ sudo docker run -it --volumes-from dbdata --name db2 ubuntu
root@b9e73847109e:/# ls
bin  boot  dbdata  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@b9e73847109e:/# cd dbdata
root@b9e73847109e:/dbdata# la
aa
root@b9e73847109e:/dbdata# ls
aa
root@b9e73847109e:/dbdata# cat aa
123
222
root@b9e73847109e:/dbdata# echo 333 >> aa 
root@b9e73847109e:/dbdata# ls
aa
```