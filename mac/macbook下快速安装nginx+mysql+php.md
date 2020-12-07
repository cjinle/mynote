# macbook下快速安装nginx+mysql+php

Mac系统是非常优秀的系统，没有之一。

自然安装起`PHP`相关的开发环境来讲也是深圳速度。

废话不多说，直接开始。


### 安装步骤
```bash
brew install nginx
brew install mysql@5.6
brew install php71
```

好了，完成了。哈哈，就几条命令

### 管理也很简单：
```bash
brew services start nginx
brew services start mysql@5.6
brew services start php71
```
