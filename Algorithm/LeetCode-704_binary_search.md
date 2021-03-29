

## LeetCode-704：二分查找

**题目**：给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

**解题思路**

1. 找到数组中间的数字。
2. 如果该数字大于目标数字，那么查找上一半的数组重复步骤1.
3. 如果该数字小于目标数字，那么查找下一半的数组重复步骤1.
4. 如果该数字等于目标数字，那么就返回下标。
5. 重复以上步骤后发现没有符合的，那么就返回-1.

**时间复杂度O($log_2n$)，以下代码可提交至LeetCode：**

[https://leetcode-cn.com/problems/binary-search/](https://leetcode-cn.com/problems/binary-search/)

```python
class Solution:
    def search(self, nums: list, target: int) -> int:

        low = 0
        hight = len(nums) - 1

        while low <= hight:
            mid = int((low + hight) / 2)
            guess = nums[mid]

            if guess == target:
                return mid
            elif guess > target:
                hight = mid - 1
            else:
                low = mid + 1

        return -1

if __name__ == '__main__':

    nums = [i for i in range(10000)]
    target = 4567

    solution = Solution()
    n = solution.search(nums, target)
    print(f'查找到数字{target}的下标为：{n}')
```

输出为:

```
查找到数字4567的下标为：4567
```



![](https://gitee.com/kkweishe/images1/raw/master/ML/2020-2-14_10-42-38.png)
