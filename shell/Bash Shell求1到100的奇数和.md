# Bash Shell求1到100的奇数和


下面是写两种方法

## 方法1
```sh
#!/bin/bash

total=0
for i in `seq 100`
do
	[ $[$i%2] -ne 0 ] &&  total=$[$total+$i]
done
echo $total
```


## 方法2
```sh
#!/bin/bash
sum=0
for ((i=1;i<101;i+=2))
do
	sum=$[$sum+$i]
done
echo $sum
```

结果都是`2500`，当然可以实现的方法还有多种
