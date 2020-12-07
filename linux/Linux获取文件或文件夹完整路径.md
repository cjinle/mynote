# Linux获取文件或文件夹完整路径

在shell脚本中，经常需要通过一个文件，获取文件当前的路径和以此文件目录再转到相关的其它目录，可以通过`readlink`命令去获取，看下面的遝

```
[root@dev test]# readlink -f dwz/index.html
/media/sf_wwwroot/test/dwz/index.html
[root@dev test]# dirname `readlink -f dwz/index.html`
/media/sf_wwwroot/test/dwz
[root@dev test]# dirname $(readlink -f dwz/index.html)
/media/sf_wwwroot/test/dwz
[root@dev test]# dirname $(readlink -f dwz/../../yii/index.php)
/media/sf_wwwroot/yii
[root@dev test]# 
```