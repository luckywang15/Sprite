### 轮转数组
> 找准轮转点，列表切片合并即可
> 当所给移动次数大于列表本身长度，则需要模运算
>> 即：当` k > n `时,轮转点就是` n - k % n`
>> 当` k <= n `时，轮转点为` n - k`

```python
def rotate(nums: List[int], k: int) -> None:
    n = len(nums)
    k = k % n
    nums[:] = nums[n-k:] + nums[:n-k]
```