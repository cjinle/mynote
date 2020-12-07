# 利用seq进行序列运算

`seq`命令可以输出一个递增的序列
如：

```
[root@localhost /]# seq 5
1
2
3
4
5
[root@localhost /]# seq -s + 5
1+2+3+4+5
[root@localhost /]# seq -s \* 5
1*2*3*4*5

```

由上面的例子可以得出，可以利用输出的序列再作运算就可以了
如：加，减，乘，除等

```
[root@localhost /]# echo $[`seq -s + 5`]
15
[root@localhost /]# echo $[`seq -s \* 5`]
120

```

**注：** 上面*在操作会转义，所以要用\*

