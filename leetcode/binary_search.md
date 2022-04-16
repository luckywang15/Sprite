### 二分法
> 二分法是用于查找有序序列中某个元素的常用方法，时间复杂度为log(n)，本身不难，但是需要对边界有一个清晰的认识
> 而且为了防止溢出，mid最好使用` mid = left + (right - left) // 2` 来实现，等价于` (left + right) // 2`

容易出错的地方：
* ` while`循环的小于号要不要带等于
* ` left`和` right`要不要加一减一

两种情况（以升序列表为例）：

* 左闭右开型区间定义
> 首先需要明确列表的索引是` 0 到 len[list]-1`
> 定义左边界` left = 0`，右边界为` right = len(list)`
> 这种情况` while`的小于号不用带等于（若带等于，则当查找到右边界，数组会越界）
```python
def binary_search(lst,target):
    left,right = 0,len(lst)
    while left < right:
        mid = left + (right - left) // 2
        if lst[mid] == target:
            return mid
        elif lst[mid] > target:
            right = mid # 右开
        elif lst[mid] < target:
            left = mid + 1 #左闭
        else:
            return mid # 找到返回下标
    return -1 # 未找到返回-1
```

* 左闭右闭型区间定义
> 定义左边界` left = 0`，右边界为` right = len(list) - 1`
> 这种情况` while`循环需要带上等于号（即使查找到达右边界，也不会发生越界）
> ` left`和` right`正常加一减一
```python
def binary_search(lst,target):
    left,right = 0,len(lst) - 1
    while left <= right:
        mid = left + (right - left) // 2
        if lst[mid] == target:
            return mid
        elif lst[mid] > target:
            right = mid - 1
        elif lst[mid] < target:
            left = mid + 1 
        else:
            return mid
    return -1 
```




### 总结
> 闭边界正常加减1
> 开边界则不用
> 建议使用左闭右闭，不易出错
