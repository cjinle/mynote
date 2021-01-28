# openssl加密解密

```php
$pri_key = file_get_contents('./pri.pem');
$pub_key = file_get_contents('./pub.pem');

$pri_handle = openssl_pkey_get_private($pri_key);
$pub_handle = openssl_pkey_get_public($pub_key);


$data = "123123123111111111111111";
$sig = sha1($data);
echo sprintf("sig: %s\n", $sig);

$aa = openssl_sign($data, $sig, $pri_key, OPENSSL_ALGO_SHA1);
var_dump($aa);
echo sprintf("openssl sig: %s\n", base64_encode($sig));



$aa = openssl_verify($data, $sig, $pub_handle, OPENSSL_ALGO_SHA1); // 1验证成功
var_dump($aa);
```