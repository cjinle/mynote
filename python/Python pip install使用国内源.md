# Python pip install使用国内源

有没有经常用pip install 某个Python扩展库的时候，
总是非常的慢，这个还不算什么，经常是装不了，这和我朝的环境有关系。。。你懂的。

所以指定一下国内的python源，就可以完美解决这个问题。

### 配置与例子
```
pip install readline -i http://pypi.douban.com/simple
```

如果要默认就指定国内源，则需要修改一下配置
**vim ~/.pip/pip.conf**
```config
[global]
index-url = http://pypi.douban.com/simple
```

下面还是几个常用的源：
http://pypi.douban.com/  豆瓣
http://pypi.hustunique.com/  华中理工大学
http://pypi.sdutlinux.org/  山东理工大学
http://pypi.mirrors.ustc.edu.cn/  中国科学技术大学
