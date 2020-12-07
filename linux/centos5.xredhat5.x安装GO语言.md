# centos5.x/redhat5.x安装GO语言

现在GO语言比较火， 自己也兴趣学习。下面是centos5.x安装GO语言过程

### 下载安装包
```
wget https://storage.googleapis.com/golang/go1.2.2.linux-amd64.tar.gz
```

### 解压安装
```
tar xzvf go1.2.2.linux-amd64.tar.gz -C /usr/local/
```

在你的PATH变量加上`:/usr/local/go/bin`环境变量
如下面的示例
**vim ~/.bash_profile**
```
PATH=$PATH:/usr/local/php/bin:/usr/local/mysql/bin:/usr/local/go/bin
```

保存完成后，记得重新加载一下环境变量` source ~/.bash_profile`

这样就可以正常使用了。

### 测试脚本
**vim hello.go**
```c
package main

import "fmt"

func main() {
    fmt.Printf("hello world!\n")
}
```

**执行：**
```
go run hello.go
```
