# PHP冒泡算法


直接上代码

```php
<?php
/**
 * 冒泡排序
 * @param array $arr
 */
function bulle_sort($arr) {
	$cnt = count($arr);
	for ($i = 0; $i < $cnt - 1; $i++) {
		for ($j = $cnt - 1; $j > $i; $j--) {
			if ($arr[$i] > $arr[$j]) {
				$temp = $arr[$i];
				$arr[$i] = $arr[$j];
				$arr[$j] = $temp;
			}
		}
	}
	return $arr;
}

$arr = array(0,8,6,1,2,3,5,7);
$out = bubble_sort($arr);
print_r($arr);
// Array ( [0] => 0 [1] => 1 [2] => 2 [3] => 3 [4] => 5 [5] => 6 [6] => 7 [7] => 8 )
?>
```