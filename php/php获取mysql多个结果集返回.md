# php获取mysql多个结果集返回

通常在开发时，`mysql`都是返回一个结果集，但如果多个结果集的话，
就需要做特殊处理。如下面代码所示：

```php
$conn = mysqli_connect('127.0.0.1', 'root', '', 'test', 3306);
$sql = "sql * from tbxx where 1";
$aa = getMultiResult($sql, $conn);
var_dump($aa);



function getMultiResult($query, $conn) {

$ret = [];
if ($conn->real_query($query)) {
	do {
		if ($result = $conn->store_result()) {
			while ($row = $result->fetch_assoc()) {
				array_push($ret, $row);
			}
		}
	} while ($conn->more_results() && $conn->next_result());
}
return $ret;
}
```

