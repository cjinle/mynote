# Python操作MySQL简单实例

运行下面的代码，你需要准备：
python运行环境及MySQLdb的python库
MySQL及一个名字`test`的数据库＋`table1`表

```python
#!/usr/bin/python
#Filename: aa.py
import os, sys, string
import MySQLdb

con = MySQLdb.connect(host='localhost',user='root',passwd='',db='test')
cursor = con.cursor()

sql = "SELECT * FROM table1 WHERE 1"

cursor.execute(sql)
data = cursor.fetchall()

if data:
  for rec in data:
    print rec[0], rec[1]
    
cursor.close()
con.close()
```

__输出结果：__

循环输出table1的字段1和字段2