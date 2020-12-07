# Python字符串快速反转(str reverse)

突然想到一个怎么快速把字符串反转输出呢？

下面有两个方法可供参考，最优为第一种方法：

### 方法一：
```python
print 'hello world'[::-1]
```

### 方法二：
```python
print ''.join(reversed('hello world'))
```