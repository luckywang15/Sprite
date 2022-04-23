### 反转链表
> 思路：一个头插解决问题
```python 
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        # 先初始化一个空的头节点，然后使用头插法
        reverse = ListNode()
        while head:
            s = head
            head = head.next # 千万要赶紧将结点推向链表下一个节点，否则下面两句又会出错，造成超时
            s.next = reverse.next
            reverse.next = s
            
        return reverse.next
```