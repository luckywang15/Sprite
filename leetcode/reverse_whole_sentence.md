### 反转字符串中的单词
> 利用切片可以实现很优雅的反转方式（string类型可像列表一样切片）

先给出自己第一次的实现方式
```python
class Solution:
    def reverseWords(self, s: str) -> str:
        a = s.split(' ') # 将字符串按照空格分隔成列表
        b = [] # 用以保存a中单个单词拆分成逐个字母的列表
        c = [] # 保存反转后的所有单词的列表
        for i in a:
            left = 0
            right = len(i) - 1
            for j in i:
                b.append(j)
            while left < right:
                b[left],b[right] = b[right],b[left]
                left += 1 
                right -= 1
            c.append(''.join(b))
            b = []
        s = ' '.join(c) # 重新连接成以空格分隔的字符串
        return s
```
然而这种思路还有更简洁的写法（列表推导式` [表达式 for 变量 in 列表]`或` [表达式 for 变量 in 列表 if 条件]`）
```python
" ".join([word[::-1] for word in s.split(" ")])
```

优雅的实现方式
> 首先，` s.split(" ")`将字符串分割成单词列表
> 然后，` s.splite(" ")[::-1]`对单词列表使用切片反转
> 更进一步,` ' '.join(s.splite(" ")[::-1])`使用join重新将单词反转之后的列表连接成以空格分隔的整句
> 最后，对整个字符串做一次切片反转

```python
" ".join(s.split(" ")[::-1])[::-1] # 使用两次切片反转
```