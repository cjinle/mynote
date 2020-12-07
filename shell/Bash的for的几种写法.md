# Bash的for的几种写法


```sh
#!/bin/bash

for i in 1 2 3 4 5
do
	echo -en "$i\n"
#	sleep 1
done 
echo

for i in `seq 5`
do	
	echo -en "$i\t"
done
echo 

for i in $(seq 5)
do	
	echo -en "$i\t"
done
echo 

for ((i=2;i<6;i++))
do
	echo -en "$i\t"
done
echo

for i in {5..10}
do
	echo -n "$i "
done
echo

for i in {a..f}
do
	echo -n "$i "
done
echo
for i in {A..Z}
do
	echo -n "$i "
done
echo

for i in /etc/*
do
	echo $i
done
echo

for i in `find /etc/ -name "*.conf"`
do
	echo $i
done
echo

find /etc/ -name "*.conf" | while read i
do
	echo $i
done
echo

`find /etc/ -name "*.conf"` | xargs echo > /tmp/find.txt
while read i 
do
        echo $i
done < /tmp/find.txt
```