## Inverview4：二维数组中的查找

**题目**：在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。存在输出True，不存在输出False。

1. 首先选取数组中右上角的数字。如果该数字等于要查找的数字，则查找过程结束；
2. 如果该数字大于要查找的数字，则剔除这个数字所在的列；
3. 如果该数字小于要查找的数字，则剔除这个数字所在的行。

```python

## start
def two_array_research(two_array, research_num):
    if len(two_array) == 0:
        print('输入数组不合规！')
        return
    
    row_n = 0
    column_n = len(two_array[0]) - 1
    flag = True
    
    while flag:
        if two_array[row_n][column_n] == research_num:
            print('True')
            flag = False
        elif two_array[row_n][column_n] > research_num:
            column_n = column_n - 1
        elif two_array[row_n][column_n] < research_num:
            row_n += 1
            
        ## 判断下标是否越界
        if row_n >= len(two_array) or column_n < 0:
            print('False')
            flag = False
    

two_array = [[1,2,8,9], [2,4,9,12], [4,7,10,13], [6,8,11,15]]
research_num = 15
two_array_research(two_array, research_num)
```

True

**Inverview4测试用例**

```python
## 二维数组中包含查找的数字（查找的数字是数组中的最大值和最小值；查找的数字介于数组中的最大值和最小值之间）。
two_array = [[1,2,8,9], [2,4,9,12], [4,7,10,13], [6,8,11,15]]
research_num = 15
two_array_research(two_array, research_num)

research_num = 1
two_array_research(two_array, research_num)

research_num = 7
two_array_research(two_array, research_num)


## 二维数组中没有查找的数字（查找的数字大于数组中的最大值；查找的数字小于数组中的最小值；查找的数字在数组的最大值和最小值之间但数组中没有这个数字）。
two_array = [[1,2,8,9], [2,4,9,12], [4,7,10,13], [6,8,11,15]]
research_num = 16
two_array_research(two_array, research_num)

research_num = 0
two_array_research(two_array, research_num)

research_num = 3
two_array_research(two_array, research_num)

## 输入空数组
two_array = []
research_num = 15
two_array_research(two_array, research_num)
```

True

True

True

False

False

False

输入数组不合规！

------

> 作者：[@mantchs](https://github.com/NLP-LOVE/ML-NLP)
>
> GitHub：[https://github.com/NLP-LOVE/CodingInterviews2-ByPython](https://github.com/NLP-LOVE/CodingInterviews2-ByPython)
>
> 有意向一起完成此项目或者有问题、有补充的可以加入《剑指offer》讨论群【818185620】<a target="_blank" href="//shang.qq.com/wpa/qunwpa?idkey=8c188e86e0eac4a214861c2c706a9c0baf75176e16e52f07b8a64d1a13f99a0d"><img border="0" src="http://pub.idqqimg.com/wpa/images/group.png" alt="《剑指offer》讨论群" title="《剑指offer》讨论群"></a>
