# Python list反转的几个实现方式

下面有几个不同实现的函数

```python
import math

def resv(li):
    new = []
    if li:
        cnt = len(li)
        for i in range(cnt):
            new.append(li[cnt-i-1])
    return new

def resv2(li):
    li.reverse()
    return li

def resv3(li):
    hcnt = int(math.floor(len(li)/2))
    tmp = 0
    for i in range(hcnt):
        tmp = li[i]
        li[i] = li[-(i+1)]
        li[-(i+1)] = tmp
    return li

li = [1, 2, 3, 4, 5]

print resv(li)
```

**ps:** `resv2()` 方法会改变原来list的排序，其它则不会
