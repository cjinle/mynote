# bash shell快速生成01,02..20字符串


### 方法1：
```bash
printf "%02d\n" `seq 20`
```

### 方法2：
```bash
seq -w 20
```

