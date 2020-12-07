# lua要点

这篇文章只记录要点，完整概念请查看官方文档

## 数据类型
```
nil, boolean, number, string, function, userdata, thread, table
```



## 三目去处符号

```lua
a, b = 1, 2
print(a > b and true or false)
```


## 数组长度问题

```lua
a = {1, 2, 3, 4}
print(#a) -- 4
a = {1, nil, 2, nil}
print(#a)  -- 1
print(table.maxn(a)) -- 3
```

## 判断

```lua
a, b = 1, 2
if a > b then
	print(a)
elseif a < b then
	print(b)
else
	print(a)
end
```


## 循环迭代

```lua
a = {1, 2, 3, 4}
for i=1,#a do
	print(a[i])
end

a = {x=1,3,4,5}
for k, v in pairs(a) do
	print(k.."="..a[k])
end

a = {x=1,3,4,5}
for k, v in ipairs(a) do
	print(k.."="..a[k])
end

a, b = 1, 10
while a < b do
	print(a)
	a = a + 1
end

a, b = 1, 10
repeat
	print(a)
	a = a + 1
until a > b 
```
