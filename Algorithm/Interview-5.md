## Inverview5：字符串替换空格

**题目**：请实现一个函数，把字符串中的每个空格替换成“%20”。例如，输入“We are happy.”，则输出“We%20are%20happy.”。

1. 首先遍历输入字符串有多少个空格。
2. 根据空格数可以计算新字符串的长度，并且创建该长度的数组
3. 再次遍历字符串，如果碰到空格，就把空格前面的字符串赋给新数组，并添加上需要替换空格的字符。
4. 把新创建的数组变换成字符串。

**时间复杂度：O(n)**

```python

## start
def replace_space_str(input_str, replace_str):
    
    if input_str == '' or input_str == None or replace_str == None:
        print('输入字符串不合法！')
        return
    
    ##遍历输入字符串找出空格数
    space_num = 0
    for char in input_str:
        if char == ' ':
            space_num += 1
    
    ## 创建新字符串数组
    new_len = len(input_str) + (len(replace_str) - 1) * space_num
    new_str = new_len * [None]
    
    index = 0
    index_new_str = 0
    for i in range(len(input_str)):
        if input_str[i] == ' ':
            ri_index_new_str = index_new_str + i - index
            
            new_str[index_new_str : ri_index_new_str] = list(input_str[index : i])
            new_str[ri_index_new_str : ri_index_new_str + len(replace_str)] = list(replace_str)
            index_new_str = ri_index_new_str + len(replace_str)
            index = i + 1
        
        if i == len(input_str) - 1:
            new_str[index_new_str : len(new_str)] = list(input_str[index : i + 1])
            
    
    print(''.join(new_str))

input_str = 'We are happy.'
replace_str = '%20'
replace_space_str(input_str, replace_str)
```

We%20are%20happy.

**Inverview5测试用例**

```python
## 输入的字符串中包含空格（空格位于字符串的最前面；空格位于字符串的最后面；空格位于字符串的中间；字符串中有连续多个空格）。
input_str = ' We are  happy. '
replace_str = '%20'
replace_space_str(input_str, replace_str)

## 输入的字符串中没有空格。
input_str = 'Wearehappy.'
replace_str = '%20'
replace_space_str(input_str, replace_str)

## 字符串是None
input_str = None
replace_str = '%20'
replace_space_str(input_str, replace_str)

## 字符串是空串
input_str = ''
replace_str = '%20'
replace_space_str(input_str, replace_str)

## 字符串只有一个空格字符
input_str = ' '
replace_str = '%20'
replace_space_str(input_str, replace_str)
```

%20We%20are%20%20happy.%20

Wearehappy.

输入字符串不合法！

输入字符串不合法！

%20

------

> 作者：[@mantchs](https://github.com/NLP-LOVE/ML-NLP)
>
> GitHub：[https://github.com/NLP-LOVE/CodingInterviews2-ByPython](https://github.com/NLP-LOVE/CodingInterviews2-ByPython)
>
> 有意向一起完成此项目或者有问题、有补充的可以加入《剑指offer》讨论群【818185620】<a target="_blank" href="//shang.qq.com/wpa/qunwpa?idkey=8c188e86e0eac4a214861c2c706a9c0baf75176e16e52f07b8a64d1a13f99a0d"><img border="0" src="http://pub.idqqimg.com/wpa/images/group.png" alt="《剑指offer》讨论群" title="《剑指offer》讨论群"></a>
