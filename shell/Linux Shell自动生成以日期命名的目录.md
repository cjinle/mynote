# Linux Shell自动生成以日期命名的目录

## 直接看代码：

```sh
#!/bin/bash

NOW=`date +%s`

for ((i=0; i<365; i++));
do
  NOW2=$((NOW+$((i*86400))));
  FILE_NAME=`date -d "1970-01-01 UTC $NOW2 seconds" +%Y-%m-%d`;
  mkdir $FILE_NAME;
done;
```

