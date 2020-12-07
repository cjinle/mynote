# gcc: readline/libreadline.a: No such file or directory 问题解决

在安装pip install readline的时候，出现了
`gcc: readline/libreadline.a: No such file or directory`
的报错。

**解决方法：**
```
yum install readline-devel
yum install patch
```

然后就可以：
```
pip install readline
pip install ipython
```