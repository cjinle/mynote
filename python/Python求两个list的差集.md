# Python求两个list的差集

如有下面两个数组：
```python
a = [1,2,3]
b = [2,3]
```

想要的结果是`[1]`

下面记录一下三种实现方式：
**1. 正常的方式**

```python
ret = []
for i in a:
    if i not in b:
        ret.append(i)

```

**2. 浓缩版**
```python
ret = [ i for i in a if i not in b ]
```

**3. 另一版**

```python
ret = list(set(a) ^ set(b))
```

个人更喜欢第三种实现方式