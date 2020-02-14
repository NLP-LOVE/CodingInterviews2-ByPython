## 目录
- [Inverview3-1：找出数组中重复的数字](#inverview3-1找出数组中重复的数字)
- [Inverview3-2：不修改数组找出重复的数字](#inverview3-2不修改数组找出重复的数字)

## Inverview3-1：找出数组中重复的数字

**题目**：在一个长度为 n 的数组里的所有数字都在 0 ~ n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。例如，如果输入长度为7的数组{2,3, 1,0,2,5,3}，那么对应的输出是重复的数字2或者3。

- 按照数组下标取数的时间复杂度为 O(1)

**解题思路**

1. 从头到尾依次扫描这个数组中的每个数字。
2. 当扫描到下标为 i 的数字时，首先比较这个数字(用 m 表示)是不是等于 i，如果是，则接着扫描下一个数字;如果不是，则再拿它和第 m 个数字进行比较。
3. 如果它和第 m 个数字相等，就找到了一个重复的数字(该数字在下标为 i 和 m 的位置都出现了);
4. 如果它和第 m 个数字不相等，就把第 i 个数字和第 m 个数字交换，把 m 放到属于它的位置。接下来再重复这个比较、交换的过程，直到我们发现一一个重复的数字。

**时间复杂度 O(n)，空间复杂度 O(1)**

```python
from typing import List

class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        self.result = []
        self.flag = True

        for i in range(len(nums)):
            if self.flag:
                self.compare(i, nums)
            else:
                return

        if self.flag:
            print('重复数字为：', self.result)
            if len(self.result) != 0 : return(self.result[0])
        
        
    ## 定义比较函数
    def compare(self, i, nums):

        if nums[i] == i:
            pass
        else:
            ## 异常判断
            try:
                if nums[i] == nums[nums[i]]:
                    self.result.append(nums[i])
                else:
                    temp = nums[i]
                    nums[i] = nums[nums[i]]
                    nums[temp] = temp
                    self.compare(i, nums)

            except:
                print('输入数组不合规！')
                self.flag = False

input_array = [2, 3, 1, 0, 2, 5, 5]
s = Solution()
s.findRepeatNumber(input_array)
```

输出为:

```
重复数字为： [2, 5]
```



**Inverview3-1测试用例**

```python
## 长度为n的数组里包含一个或者多个重复的数字
input_array = [4,3,2,4,5,5]
s.findRepeatNumber(input_array)

## 数组中不包含重复数字
input_array = [4,1,2,0,5,3,6]
s.findRepeatNumber(input_array)

## 无效输入测试用例--空数组
input_array = []
s.findRepeatNumber(input_array)

## 无效输入测试用例--长度为n的数组中包含0——n-1 之外的数字
input_array = [1,7,1,2,2]
s.findRepeatNumber(input_array)
```

输出为:

```
重复数字为： [5, 4]
重复数字为： []
重复数字为： []
输入数组不合规！
```



## Inverview3-2：不修改数组找出重复的数字

**题目**：在一个长度为 n+1 的数组里的所有数字都在 1~n 的范围内，所以数组中至少有一个数字是重复的。请找出数组中任意一个重复的数字，但不能修改输入的数组。例如，如果输入长度为8的数组{2,3,5,4,3,2,6,7}，那么对应的输出是重复的数字2或者3。

**解题思路**

1. 我们把从 1\~n 的数字从中间的数字 m 分为两部分，前面一半为 1\~m,后面一半为 m+1\~n。
2. 如果 1\~m 的数字的数目超过 m ,那么这一半的区间里一定包含重复的数字;否则，另一半 m+1\~n 的区间里一定包含重复的数字。
3. 我们可以继续把包含重复数字的区间一分为二，直到找到一个重复的数字。

代码按照二分查找的思路，如果输入长度为 n 的数组，那么遍历数组将被调用 O(logn) 次，每次需要 O(n) 的时间，因此总的时间复杂度是 O(nlogn) ,空间复杂度为 0(1) 。和最前面提到的需要 0(n) 的辅助空间的算法相比，这种算法相当于以时间换空间。

```python
from typing import List

class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        if len(nums) == 0:
            print('输入数组不合法！')
            return
        
        start_n = 1
        end_n = len(nums) - 1
        flag = True

        ## 循环
        while flag:
            middle = int((end_n - start_n) / 2)
            if middle == 0:
                flag = False
            middle = start_n + middle
            left_n = 0
            right_n = 0

            ## 开始比较数字，分区域统计
            for num in nums:
                if num <= middle and num >= start_n:
                    left_n += 1
                elif num > middle and num <= end_n:
                    right_n += 1
                elif end_n + start_n == len(nums):
                    print('输入数组不合法！')
                    flag = False

            ## 两边区域个数比较
            if left_n > middle - start_n + 1:
                end_n = middle
                if flag == False:
                    print('重复数字为：',start_n)
            elif right_n > end_n - middle:
                start_n = middle + 1
                if flag == False:
                    print('重复数字为：',end_n)

input_array = [2, 3, 5, 3, 4, 6, 3, 7]
s = Solution()
s.findRepeatNumber(input_array)
```

结果如下:

```
重复数字为： 3
```



**Inverview3-2测试用例**

```python
## 长度为n的数组里包含一个或者多个重复的数字
input_array = [2, 3, 5, 4, 1, 4, 3, 7]
s.findRepeatNumber(input_array)

## 数组中不包含重复数字
input_array = [2, 3, 5, 4, 1, 6, 8, 7]
s.findRepeatNumber(input_array)

## 输入空数组
input_array = []
s.findRepeatNumber(input_array)
```

结果如下:

```
重复数字为： 3
输入数组不合法！
输入数组不合法！
```
