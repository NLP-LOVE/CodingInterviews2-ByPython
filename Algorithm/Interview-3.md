## 目录
- [Inverview3-1：找出数组中重复的数字](#inverview3-1找出数组中重复的数字)
- [Inverview3-2：不修改数组找出重复的数字](#inverview3-2不修改数组找出重复的数字)

## Inverview3-1：找出数组中重复的数字

**题目**：在一个长度为 n 的数组里的所有数字都在 0 ~ n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。例如，如果输入长度为7的数组{2,3, 1,0,2,5,3}，那么对应的输出是重复的数字2或者3。

- 按照数组下标取数的时间复杂度为 O(1)

1. 从头到尾依次扫描这个数组中的每个数字。
2. 当扫描到下标为 i 的数字时，首先比较这个数字(用 m 表示)是不是等于 i，如果是，则接着扫描下一个数字;如果不是，则再拿它和第 m 个数字进行比较。
3. 如果它和第 m 个数字相等，就找到了一个重复的数字(该数字在下标为 i 和 m 的位置都出现了);
4. 如果它和第 m 个数字不相等，就把第 i 个数字和第 m 个数字交换，把 m 放到属于它的位置。接下来再重复这个比较、交换的过程，直到我们发现一一个重复的数字。

**时间复杂度 O(n)，空间复杂度 O(1)**

```python
## start
## 循环数组
def start(input_array):
    start.result = '重复数字为：'
    start.flag = True
    
    for i in range(len(input_array)):
        if start.flag:
            compare(i)
        else:
            return
        
    print(start.result)


## 定义比较函数
def compare(i):
    global result
    
    if input_array[i] == i:
        pass
    else:
        ## 异常判断
        try:
            if input_array[i] == input_array[input_array[i]]:
                start.result = start.result + str(input_array[i]) + ','
            else:
                temp = input_array[i]
                input_array[i] = input_array[input_array[i]]
                input_array[temp] = temp
                compare(i)
                
        except:
            print('输入数组不合规！')
            start.flag = False


input_array = [2, 3, 1, 0, 2, 5, 3]
start(input_array)
            
```

重复数字为：2,3,

**Inverview3-1测试用例**

```python
## 长度为n的数组里包含一个或者多个重复的数字
input_array = [4,3,2,4,5,5]
start(input_array)

## 数组中不包含重复数字
input_array = [4,1,2,0,5,3,6]
start(input_array)

## 无效输入测试用例--空数组
input_array = []
start(input_array)

## 无效输入测试用例--长度为n的数组中包含0——n-1 之外的数字
input_array = [1,7,1,2,2]
start(input_array)
```

重复数字为：5,4,

重复数字为：

重复数字为：

输入数组不合规！



## Inverview3-2：不修改数组找出重复的数字

**题目**：在一个长度为 n+1 的数组里的所有数字都在 1~n 的范围内，所以数组中至少有一个数字是重复的。请找出数组中任意一个重复的数字，但不能修改输入的数组。例如，如果输入长度为8的数组{2,3,5,4,3,2,6,7}，那么对应的输出是重复的数字2或者3。

1. 我们把从 1~n 的数字从中间的数字 m 分为两部分，前面一半为 1~m,后面一半为 m+1~n。
2. 如果 1~m 的数字的数目超过 m ,那么这一半的区间里一定包含重复的数字;否则，另一半 m+1~n 的区间里一定包含重复的数字。
3. 我们可以继续把包含重复数字的区间一分为二，直到找到一个重复的数字。

代码按照二分查找的思路，如果输入长度为 n 的数组，那么遍历数组将被调用 O(logn) 次，每次需要 O(n) 的时间，因此总的时间复杂度是 O(nlogn) ,空间复杂度为 0(1) 。和最前面提到的需要 0(n) 的辅助空间的算法相比，这种算法相当于以时间换空间。

```python

## start
def start(input_array):
    if len(input_array) == 0:
        print('输入数组不合法！')
        return
    start_n = 1
    end_n = len(input_array) - 1
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
        for num in input_array:
            if num <= middle and num >= start_n:
                left_n += 1
            elif num > middle and num <= end_n:
                right_n += 1
            elif end_n + start_n == len(input_array):
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
            

input_array = [2, 3, 5, 4, 1, 6, 3, 7]
start(input_array)
```

重复数字为： 3

**Inverview3-2测试用例**

```python
## 长度为n的数组里包含一个或者多个重复的数字
input_array = [2, 3, 5, 4, 1, 4, 3, 7]
start(input_array)

## 数组中不包含重复数字
input_array = [2, 3, 5, 4, 1, 6, 8, 7]
start(input_array)

## 输入空数组
input_array = []
start(input_array)
```

重复数字为： 3

输入数组不合法！

输入数组不合法！



------

> 作者：[@mantchs](https://github.com/NLP-LOVE/ML-NLP)
>
> GitHub：[https://github.com/NLP-LOVE/CodingInterviews2-ByPython](https://github.com/NLP-LOVE/CodingInterviews2-ByPython)
>
> 有意向一起完成此项目或者有问题、有补充的可以加入《剑指offer》讨论群【818185620】<a target="_blank" href="//shang.qq.com/wpa/qunwpa?idkey=8c188e86e0eac4a214861c2c706a9c0baf75176e16e52f07b8a64d1a13f99a0d"><img border="0" src="http://pub.idqqimg.com/wpa/images/group.png" alt="《剑指offer》讨论群" title="《剑指offer》讨论群"></a>
