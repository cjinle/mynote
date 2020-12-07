# php的include_once,require_once值得注意的小细节

人往往有种先入为主，觉得事情会和自己想像中的发展，
但很多时候事与愿违。编程也一样，和今天讲的这个小细节有关

### 举个例子

**inc.php**

```php
<?php
return array(
	'foo'=>'bar',
);
```


**test.php**
```php
<?php
$cfg = include_once('inc.php');
var_dump($cfg);
$cfg = include_once('inc.php');
var_dump($cfg);
```

![php-include](/uploads/2016/10/php-include.png)
### 运行
```php
[root@localhost ~]# php test.php 
array(1) {
  ["foo"]=>
  string(3) "bar"
}
bool(true)
```

事实上，第二个返回的结果，相信有些出乎意料。
当一个文件`include_once`过之后，再执行的时候，返回是`bool`值，
意思是这个文件已经被包含过了，而不是你想要的返回的配置数组。

当然可以用`include`来解决这个问题，但如果在一个常驻脚本上，
无限`include`的话，是否会占用内存越来越大，导致内存泄漏，值得深究下去。