### 1.给出一个只有数字的列表，然后再给一个数k，求让列表中所有小于等于k的数都相邻所需要的交换次数
```python
while True:
    try:
        # 思路：直接比较每个长度固定的滑动窗口内大于k的个数，输出最少的那一个即可
        a = list(map(int, input('').split(' ')))
        k = int(input(''))
        n = 0 # 小于k的整数的个数
        res = [] # 记录交换次数的列表
        for i in a:
            if i < k:
                n += 1
        for i in range(len(a) - n + 1):
            temp = 0
            for j in a[i:i+n]:
                if j >= k:
                    temp += 1
            res.append(temp)
        print(min(res))
        print(len(a) - n + 1)
    except:
        break
```
### 2.给出一个只包含正整数的列表L，列表中每个数代表可以往列表后面走多少位，第一步可以从[0, len(L)//2]中任选一个开始走，求走到列表末尾需要的最少步数
```python
while True:
    try:
        l = list(map(int, input('').split(' ')))
        n = len(l)
        res = []
        result = n + 1
        # 思路：由于第一步步长为[1,n/2]，因此问题可以分解为找所有第一步能走到最后的最少步骤（动态规划）
        for i in range(1, n // 2):
            sum_road = i
            res.append(i)
            while sum_road < n:  # 因为数组内都是正整数而且不能往回走，所以不用考虑走不到的情况
                res.append(l[sum_road])
                sum_road += l[sum_road]
                if sum_road == n - 1:  # 走到结尾时，记录最短步数
                    result = min(result, len(res))
            res = []  # 清空res列表
        if n != 0 and result != n + 1:
            print(result)
        else:
            print('-1')

    except:
        break
```
### 3.一个骰子，初始状态为'123456'，有六种状态改变方式(L、R、F、B、S、N)，给一个状态改变方式字符串(eg:'LLRBGNS')，输出骰子最终状态
```python
def f(n):
    if n == 1:
        return 1
    elif n == 2:
        return 2
    else:
        return f(n - 1) + f(n - 2)
print(f(44))

while True:
    try:
        # 思路：以R为例，保持列表一二位不变，交换三四位并将交换后的三四位整体与五六位交换
        p = input('')  # 输入操作列表
        a = '123456'
        res = list(a)
        for i in p:
            if i == 'L':
                res = res[:2] + res[4:6] + res[2:4][::-1]
            elif i == 'R':
                res = res[:2] + res[4:6][::-1] + res[2:4]
            elif i == 'F':
                res = res[4:] + res[2:4] + res[:2][::-1]
            elif i == 'B':
                res = res[4:][::-1] + res[2:4] + res[:2]
            elif i == 'S':
                res = res[2:4][::-1] + res[:2] + res[4:]
            elif i == 'N':
                res = res[2:4] + res[:2][::-1] + res[4:]
            else:
                print('False')
                break
        print(''.join(res))
    except:
        break
```

### 4.给你一个升序排列的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。元素的 相对顺序 应该保持 一致 
```python
# nums = [1,2,2,3,4]
# 常规暴力解法
class Solution:
    def removeDuplicates(self, nums) -> int:
        sort = [nums[0]]
        for i in range(1, len(nums)):
            if sort[-1] != nums[i]:
                sort.append(nums[i])
        k = len(sort)
        nums[:k] = sort
        print(k)
# 双指针解法
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        i = 0
        j = 0
        n = len(nums)
        while j < n:
            if nums[i] == nums[j]:
                j += 1
            else:
                i += 1
                nums[i], nums[j] = nums[j], nums[i]
                j += 1
        return i+1
```
