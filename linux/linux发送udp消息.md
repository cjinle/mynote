# linux发送udp消息

假设本服务器起了一个端口为`11110`的`udp`服务

## 第一种方法

```sh
echo -n "hello" | nc -4u -w1 localhost 11110
```

## 第二种方法
```sh
echo -n "hello" > /dev/udp/localhost/11110
```

但第二种方法有一个问题，消息可以发送成功，但收不到服务器返回的消息