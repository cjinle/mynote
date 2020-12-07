# MySQL用命令导出导入数据库

MySQL的的简单数据库备份，
一般来说，都是把一个库`mysqldump`成一个.sql的脚本文件
当然这个对于小数据来讲的。

导出：
```
#mysqldump -uroot -p123 db_name > db_bak.sql
```
上面这条命令的意思是：
数据库用户名为`root`, 密码为`123`
要导出的数据库是`db_name`
导出的SQL文件叫`db_bak.sql`且此文件在当成目录生成

**导入：**

```
#mysql -uroot -p123`
mysql> use new_db;
mysql> set names utf8;
mysql> source db_bak.sql;
```
上面命令的意思是：
登录到mysql服务器
选择要导入的数据库(`use new_db`)
设置字符编码，不要问为什么，这个是为了防止乱码
编码最好一致，不然会出现莫名的错误
例如：`gbk`, `gb2312`, `utf8` ...
最后一步就是导入了，`source db_bak.sql`
`db_bak.sql`这个文件在当前目录。可以使用绝对路径来指明

