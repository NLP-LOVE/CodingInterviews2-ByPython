## Inverview-7：重建二叉树

**题目**：输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如，输入前序遍历序列{1,2,4, 7,3,5, 6, 8}和中序遍历序列{4, 7,2,1,5,3,8, 6}，则重建如下图所示的二叉树并输出它的头节点。

![](https://gitee.com/kkweishe/images/raw/master/ML/2019-8-31_8-55-28.png)

**前序遍历**：访问顺序为根节点、左子节点、右子节点。

**中序遍历**：访问顺序为左子节点、根节点、右子节点。

**后序遍历**：访问顺序为左子节点、右子节点、根节点。

根据前序遍历的特点，第一个数必定是根节点，根据中序遍历的特点，只要找到序列当中的根节点，在根节点的左边序列是左子树，在根节点的右边序列是右子树。

1. 创建一个二叉树类。
2. 编写递归函数，先写出满足最小分割的序列，也就是说如果前序遍历序列和中序遍历序列只有两个数值的时候，那么就可以得到叶子节点，并返回这个只有两层的子二叉树。
3. 如果分割的序列不只是两个数值，那么就需要继续分割子序列，递归调用，直到分割为只有两个数值为止。
4. 这也有特殊情况，也就是根节点在最后边、最左边或者是根节点的右边只有一个数值、根节点的左边只有一个数值，那么就可以构造叶子节点了。
5. 最后依次返回得到这颗二叉树。

```python

## 创建二叉树类
class Node():
    def __init__(self, item):
        self.element = item
        self.leftNode = None
        self.rightNode = None


## 构建二叉树
def struct_tree(pre_list, middle_list):
    
    if len(pre_list) == 2:
        
        # 根节点
        node = Node(pre_list[0])
        #左叶子节点
        if pre_list[0] == middle_list[1]:
            left_node = Node(pre_list[1])
            node.leftNode = left_node
        else:
            # 右叶子节点
            right_node = Node(pre_list[1])
            node.rightNode = right_node
        
        ## 添加父节点
        if node.leftNode != None:
            node.leftNode.parentNode = node
        if node.rightNode != None:
            node.rightNode.parentNode = node
            
        return node
    else:
        ## 递归调用
        for i in range(len(middle_list)):
            if middle_list[i] == pre_list[0]:
                middle_root_index = i
        
        # 根节点
        node = Node(pre_list[0])
        # 左子树
        if middle_root_index > 1:
            left_pre_list = pre_list[1 : middle_root_index + 1]
            left_middle_list = middle_list[0 : middle_root_index]
            node.leftNode = struct_tree(left_pre_list, left_middle_list)
        elif middle_root_index == 1:
            left_node = Node(middle_list[0])
            node.leftNode = left_node
        
        # 右子树
        if middle_root_index < len(pre_list) - 2:
            right_pre_list = pre_list[middle_root_index + 1 : ]
            right_middle_list = middle_list[middle_root_index + 1 : ]
            node.rightNode = struct_tree(right_pre_list, right_middle_list)
        elif middle_root_index == len(pre_list) - 2:
            right_node = Node(middle_list[len(pre_list) - 1])
            node.rightNode = right_node
        
        ## 添加父节点
        if node.leftNode != None:
            node.leftNode.parentNode = node
        if node.rightNode != None:
            node.rightNode.parentNode = node
            
        return node

pre_list = [1, 2, 4, 7, 3, 5, 6, 8]
middle_list = [4, 7, 2, 1, 5, 3, 8, 6]
node = struct_tree(pre_list, middle_list)
print('根节点：', node.element)
```

根节点： 1

**Inverview-7测试用例**

![](https://gss3.bdstatic.com/-Po3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike92%2C5%2C5%2C92%2C30/sign=b5718c5e3687e950561afb3e71513826/f9dcd100baa1cd1171faf1bdb512c8fcc2ce2dda.jpg)

```python
## 完全二叉树
pre_list = [1, 2, 4, 8, 9, 5, 10, 3, 6, 7]
middle_list = [8, 4, 9, 2, 10, 5, 1, 6, 3, 7]
node = struct_tree(pre_list, middle_list)
print('最左边的叶子节点：', node.leftNode.leftNode.leftNode)

## 不完全二叉树
pre_list = [1, 2, 4, 8, 9, 5, 10, 3, 7]
middle_list = [8, 4, 9, 2, 10, 5, 1, 3, 7]
node = struct_tree(pre_list, middle_list)
print('最右边的叶子节点：', node.rightNode.rightNode)

## 所有节点都没有右子节点的二叉树
pre_list = [1, 2, 4, 8]
middle_list = [8, 4, 2, 1]
node = struct_tree(pre_list, middle_list)
print('最左边的叶子节点：', node.leftNode.leftNode.leftNode)

## 所有节点都没有左子节点的二叉树
pre_list = [1, 3, 7]
middle_list = [1, 3, 7]
node = struct_tree(pre_list, middle_list)
print('最右边的叶子节点：', node.rightNode.rightNode)

## 只有1个节点的二叉树
pre_list = [1]
middle_list = [1]
node = struct_tree(pre_list, middle_list)
print('根节点：', node.element)
```

最左边的叶子节点： 8

最右边的叶子节点： 7

最左边的叶子节点： 8

最右边的叶子节点： 7

根节点： 1

> 作者：[@mantchs](https://github.com/NLP-LOVE/ML-NLP)
>
> GitHub：[https://github.com/NLP-LOVE/CodingInterviews2-ByPython](https://github.com/NLP-LOVE/CodingInterviews2-ByPython)
>
> 有意向一起完成此项目或者有问题、有补充的可以加入《剑指offer》讨论群【818185620】<a target="_blank" href="//shang.qq.com/wpa/qunwpa?idkey=8c188e86e0eac4a214861c2c706a9c0baf75176e16e52f07b8a64d1a13f99a0d"><img border="0" src="http://pub.idqqimg.com/wpa/images/group.png" alt="《剑指offer》讨论群" title="《剑指offer》讨论群"></a>
