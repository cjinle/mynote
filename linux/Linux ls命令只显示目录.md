# Linux ls命令只显示目录

Linux `ls`命令只显示目录， 看起来这个问题好像很简单，
但真的没几个人知道，因为自己都习惯直接`ls -lh`之类的，
就可以看到所有的可见文件或目录，或者再加个 `grep ^d`就可以出来目录
但其实有更新简单的参数，请看下面：

Linux ls命令只显示目录
```
$ ls -d */
$ echo */
```

上面两个命令都可以完美解决上面的需求。
