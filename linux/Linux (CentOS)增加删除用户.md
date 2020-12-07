# Linux (CentOS)增加删除用户

在Linux终端下如何增加删除普通用户帐户
想了解Linux下的用户信息，主要两个文件：`/etc/passwd`和`/etc/shadow`
这两个文件明天再详细解释


今天主要讲一下用命令创建和删除用户

## 增加用户
一般是两个步骤，增加用户名和指定用户密码

```
[root@localhost /]# useradd test2
[root@localhost /]# passwd test2
Changing password for user test2.
New UNIX password:
BAD PASSWORD: it does not contain enough DIFFERENT characters
Retype new UNIX password:
passwd: all authentication tokens updated successfully.


#下面这个命令是为用户指定家目录的
[root@localhost home]# useradd test5 -d /home/t
#更多详细的参数man useradd
```


## 删除用户
删除用户比较简单，默认不加参数，不会把用户的家目录删除，
要删除家目录的时候，要加上-r参数

```
#默认没有删除家目录
[root@localhost home]# userdel test2
[root@localhost home]# ls /home
lele  swap  t  t4  test2  test3

#加上-r参数可以把家目录也一并删除
[root@localhost home]# useradd test6
[root@localhost home]# ls /home
lele  swap  t  t4  test2  test3  test6
[root@localhost home]# userdel -r test6
[root@localhost home]# ls /home
lele  swap  t  t4  test2  test3

#更多参数man userdel
```

明天讲解一下，如何不用命令，手工建文件增加用户