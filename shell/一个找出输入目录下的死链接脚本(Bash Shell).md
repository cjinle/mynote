# 一个找出输入目录下的死链接脚本(Bash Shell)

下面这个脚本，只要输入目录的路径，
就可以帮你找到目录下的死链接，支持子目录查找
如输入：`/etc`

源码如下：

```sh
#!/bin/bash

#read -p "input a directory:" dir
#echo

#for i in $dir/*
#do
#      [ -h $i -a ! -e $i ] && echo "$i是死链接"
#done

read -p "input a directory:" dir
echo

find $dir -type l |while read i
do
      [ ! -e $i ] && echo "$i是死链接"
done
```