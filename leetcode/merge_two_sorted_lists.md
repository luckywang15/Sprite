### 合并两个有序链表

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        # 思路：初始化一个带头节点的空链表，最后返回不包括头结点的链表（带头结点是为了让链表操作更统一）
        head = ListNode()
        r = head # 表尾指针
        while list1 and list2:
            if list1.val <= list2.val:
                s = list1 # s为工作指针（其实也可以不要，这里是为了让尾插法更明显）
                r.next = s
                r = s
                list1 = list1.next
            else:
                s = list2
                r.next = s
                r = s
                list2 = list2.next
        # r.next = l1 if l1 else l2 # 更简洁的写法
        if list1:
            r.next = list1
        else:
            r.next = list2
        return head.next

```

最初超时的写法(修改测试之后运行正确)：
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
def mergeTwoLists(list1, list2):
    # 思路：初始化一个带头节点的空链表，最后返回不包括头结点的链表
    head = ListNode(0, None)
    r = head  # 表尾指针
    while list1 and list2:
        if list1.val < list2.val:
            s = list1
            r.next = s
            r = s
            list1 = list1.next
        elif list1.val > list2.val:
            s = list2
            r.next = s
            r = s
            list2 = list2.next
        else:
            s = list1
            r.next = s
            r = s
            list1 = list1.next  # ①
            s = list2
            r.next = s # ②
            r = s
            # list1 = list1.next # 这样写是错误的，这样会使list1复制list2的引用（因为在②步的时候r指向list1之前的地址，这句语句使list1断链了，接到list2上了，所以之后会造成超时错误）
            # 而如果把这条语句写到①处，则list1被及时指向正确的下一个结点，不会造成断链错误
            # 但是这样写也不好，因为之前的list1一直会链接到list2上面去，虽然不影响这道题目的正确性，但是还是上面那种写法更好
            list2 = list2.next
    if list1:
        r.next = list1
    else:
        r.next = list2
    return head.next
# node3 = ListNode(4, None)
# node2 = ListNode(2, node3)
# l1 = ListNode(1, node2)

# node5 = ListNode(4, None)
# node4 = ListNode(3, node5)
# l2 = ListNode(1, node4)

# print(mergeTwoLists(l1, l2))
```