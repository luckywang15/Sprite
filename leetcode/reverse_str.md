### 反转字符串
> 不需要其它语言的swap()方法，Python以引用方式管理对象，可以直接交换引用
```python
a,b = b,a
```
> 于是原地反转字符串或列表（数组）的方法如下
```python
left = 0
right = len(s) - 1
while left < right:
    s[left],s[right] = s[right],s[left]
    left += 1
    right -= 1
```