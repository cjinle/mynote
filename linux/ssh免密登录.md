# ssh免密登录

## 环境
现有服务器A `1.1.1.1`和服务器B `2.2.2.2`
现在需要A免密登录到B

## 生成密钥(服务器A)

```
ssh-keygen -t rsa -f ~/.ssh/my-ssh-key -C [USERNAME]
```

然后生成`my-ssh-key`, `my-ssh-key.pub`公私钥

然后把my-ssh-key.pub内容添加到要登录的服务器B [USERNAME]/.ssh/authorized_keys文件内

注意文件如果不存在，直接创建，authorized_keys的文件权限需要为600


然后客户端(服务器A)只要登录引用my-ssh-key即可，如：

```sh
ssh root@2.2.2.2 -i ~/.ssh/my-ssh-key
```


如果需要B也免密登录到A，则反过来操作一遍即可