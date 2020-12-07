# Shell(Bash)运算的几种写法

## 例子：

```sh
#!/bin/bash

a=1
let a++
let 'a+=2'
b=`expr $a + 3`
c=$((a+5))
d=$[a+7]

echo $a
echo $b
echo $c
echo $d
```

### 结果是：
```
4
7
9
11
```

写法虽然多种，很容易混乱，

所以只需要选择自己习惯的即可，其它的能看懂就好
