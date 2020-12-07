# php获取某个mysql数据库所有的存储过程

## 源码

```php
$sql = "SHOW PROCEDURE STATUS WHERE db = 'test'";
$arr = oo::db('config')->getAll($sql);
$ret = [];
foreach ($arr as $k => $v) {
	$ret[] = $v['Name'];
}

var_dump($ret);
```

