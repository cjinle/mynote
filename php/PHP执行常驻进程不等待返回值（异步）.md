# PHP执行常驻进程不等待返回值（异步）

```php
// "> /dev/null 2>/dev/null &"
shell_exec('php measurePerformance.php 47 844 email@yahoo.com > /dev/null 2>/dev/null &');
```