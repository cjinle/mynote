# openssl加密解密


## 根据私钥生成公钥
```
openssl rsa -in id_rsa -pubout -out cjinle.pub
```


## 加密解密数据
```
echo hello > hello.txt
openssl rsautl -sign -in hello.txt -inkey id_rsa -out sig
openssl rsautl -verify -in sig -inkey cjinle.pub -pubin
```

## 正常生成私钥和公钥

```
ssh-keygen -t rsa
```


## 根据私钥生成ssh公钥

```
ssh-keygen -y -f ~/.ssh/id_rsa > ~/.ssh/id_rsa.pub
```
