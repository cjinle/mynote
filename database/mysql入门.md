# MySQL入门

## 数字格式化

mysql的`format`函数，可以格式化数据为整数或者浮点数。

```sh
select format(100.31111,2); # 100.31
select format(100.31111,0); # 100
select format(100.51111,0); # 101
```

## MySQL给用户加库操作权限

```sh
GRANT ALL PRIVILEGES ON `DB_NAME`.* TO 'USER_NAME'@'HOST' WITH GRANT OPTION;
grant all privileges on `db`.* to 'user'@'host' identified by 123;
flush privileges; # 刷新权限
```

## 导入导出数据

### 导入数据文件到MySQL
```sh
mysql -uroot -p123`
mysql> use new_db;
mysql> set names utf8;  # 设置数据库编码
mysql> source db_bak.sql;
```
### 从MySQL导出数据文件
```sh
mysqldump -uroot -p123 db_name > db_bak.sql
```
