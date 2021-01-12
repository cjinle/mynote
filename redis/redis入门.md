# redis入门

## zset 可排序集合

```shell
zadd test 1 one
zadd test 2 two
zadd test 3 three
zadd test 4 four
zadd test 5 five

zrevrange test 0 -1 withscores

zremrangebyrank test 0 -50 
```