# php完整路径获取文件名

## 获取完整文件名
```php
$path = "/data/wwwroot/test/index.php";
echo basename($path); // 输出 index.php
```

## 获取完整文件名（不带后缀）
```php
$path = "/data/wwwroot/test/index.php";
echo basename($path, ".php"); // 输出 index
```