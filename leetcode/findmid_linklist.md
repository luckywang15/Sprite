### 给定一个头节点指向链表第一个元素的非空单链表，返回链表的中间结点
#### 如果有两个中间结点，则返回第二个中间结点

我的解决方式
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode(self, head: ListNode) -> ListNode:
        n = 0 # 记录链表长度
        l = [] # 保存链表结点，方便返回中间结点
        while head: # 遍历单链表
            n += 1
            l.append(head)
            head = head.next
        target = n // 2 
        return l[target]
```
别人更好的思路：快慢指针
> * 快指针每次走两步
> * 慢指针每次走一步
> * 当快指针走到末尾，慢指针在中间位置
```python
class Solution:
    def middleNode(self, head: ListNode) -> ListNode:
        fast = head
        slow = head
        while fast and fast.next: # 当前结点和下一结点同时非空时快结点才能指到下下个结点
            fast = fast.next.next
            slow = slow.next
        return slow
```
### 思考
> 对于快慢指针，一开始纠结于` fast = slow = head`这个赋值，因为之前搞懂了深浅拷贝，以为自己对各种变量赋值的理解不会有问题了，然而对于这个赋值的理解还是出现了问题，后来在与朋友的讨论中基本上想清楚了：
>> 首先，赋值是建立或复制对象的引用，这里的fast和slow相当于两个head所指对象的引用
>> 其次，head是链表的一个结点，fast和slow也是，每个结点对象的地址都不同，因此赋值时复制的引用也不同（这里不同于对可变对象（list/dict/set），比如对list进行修改，list对象的引用还是保持不变）
```python
dic = {'a': 1, 'b': 2}
print(id(dic)) # 2093917108736
dic['c'] = 3
print(id(dic)) # 2093917108736
```

### 总结
> 对于列表、字典和集合这些` 可变对象`，通过对变量所引用对象本身进行操作，可以只改变变量的值而不改变变量的引用；但对于数字、字符串和元组这些` 不可变对象`（小数据池内的除外），由于对象本身是不能够进行变值操作的，因此要想改变相应变量的值，就必须要新建对象，再把新建对象赋值给变量