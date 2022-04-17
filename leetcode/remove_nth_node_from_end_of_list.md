### 删除链表倒数第n个结点
1.常规思路：
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        num = 0 # 保存链表结点总数
        pre = 0 # 记录被删结点前一个结点的下标
        H = head # 保存头节点（非空）
        while head:
            num += 1
            head = head.next
        head = H
        if n == num: # 因为是非空头节点，第一个结点需要特殊处理
            head = head.next
            return head
        while head: # 找到需要删除结点的前一个结点，删除待删结点
            pre += 1 
            if pre == num - n:
                head.next = head.next.next
                return H
            head = head.next
```
2.快慢指针方法（其实应该叫前后指针）：
```python
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        prehead = ListNode(0, head) # 创建空头结点，用以统一链表上所有结点的操作
        fast = slow = prehead
        for _ in range(n): # n次操作
            fast = fast.next
        while fast.next:
            slow = slow.next
            fast = fast.next
        slow.next = slow.next.next
        return prehead.next
            
```
总结：
> 第一次尝试用前后指针的方法时，犯了一个错误，我用` H = head`，但是这无法解决要删除的就是第一个结点这种情况，因此还是使用` prehead.next`，这样一来直接统一了所有节点操作