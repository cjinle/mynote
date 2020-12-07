# MySQL给用户加库操作权限


```sql
GRANT ALL PRIVILEGES ON `DB_NAME`.* TO 'USER_NAME'@'HOST' WITH GRANT OPTION;

grant all privileges on `db`.* to 'user'@'host' identified by 123;

flush privileges; # 刷新权限
```