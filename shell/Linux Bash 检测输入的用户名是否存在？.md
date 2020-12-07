# Linux Bash 检测输入的用户名是否存在？

代码如下：

```bash
#!/bin/bash

read -p "Please input a username: " username

id $username > /dev/null 2>&1
ret=$?
if [ "$ret" -eq "0" ]; then
    echo "${username} is exist!"
else
    echo "${username} is not exist!"
fi
```

**测试：**
```
[root@rhel6 shell]# sh check_username.sh 
Please input a username: lok
lok is not exist!
[root@rhel6 shell]# sh check_username.sh
Please input a username: root
root is exist!
```