# Debian环境下pip install scrapy错误error: command 'gcc' failed with exit status 1解决


用`pip install scrapy`的时候，出现了下面的错误

```
....
src/lxml/lxml.etree.c:6:6: error: #error Python headers needed to compile C extensions,
 please install development version of Python.

error: command 'gcc' failed with exit status 1
```

### 解决方法：
```
# apt-get install python-dev libxml2-dev libxslt-dev -y
```

安装完上面的库后，再`pip install scrapy`就可以正常安装了。

### CentOS/Redhat系统

```
# yum install libxml2-devel libxslt-devel -y
```


### 其它安装scrapy记录：
```
export PKG_CONFIG=/usr/local/bin/pkg-config
export PKG_CONFIG_PATH=/usr/share/pkgconfig:/usr/lib/pkgconfig
```
如果安装cffi碰到找不到`error: ffi.h: No such file or directory`
```
ln -s /usr/local/lib/libffi-3.1/include/* /usr/local/include/
```