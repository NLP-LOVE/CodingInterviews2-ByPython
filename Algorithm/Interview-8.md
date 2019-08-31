## Inverview-8：二叉树中序遍历的下一个节点

**题目**：给定一棵二叉树和其中的一个节点，如何找出中序遍历序列的下一个节点?树中的节点除了有两个分别指向左、右子节点的指针，还有一个指向父节点的指针。这颗二叉树如下图所示：

![](https://gitee.com/kkweishe/images/raw/master/ML/2019-8-31_17-40-48.png)

1. 如果一个节点有右子树，那么它的下一个节点就是它的右子树中的最左子节点。

2. 如果节点没有右子树的情形，并且该节点是它父节点的左子节点，那么它的下一个节点就是它的父节点。

3. 如果一个节点既没有右子树，并且它还是它父节点的右子节点，那么这种情形就比较复杂。我们可以沿着指向父节点的指针一直向上遍历，直到找到一个是它父节点的左子节点的节点。如果这样的节点存在，那么这
   个节点的父节点就是我们要找的下一个节点。

   例如 i 节点，我们沿着指向父节点的指针向上遍历，先到达节点 e。由于节点 e 是它父节点 b 的右节点，我们继续向上遍历到达节点 b。节点 b 是它父节点 a 的左子节点，因此节点 b 的父节点 a 就是节点i的下一个节点。

```python

## 创建二叉树类
class Node():
    def __init__(self, item):
        self.element = item
        self.parentNode = None
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



pre_list = ['a', 'b', 'd', 'e', 'h', 'i', 'c', 'f', 'g']
middle_list = ['d', 'b', 'h', 'e', 'i', 'a', 'f', 'c', 'g']
node = struct_tree(pre_list, middle_list)

## start 查找下一个节点
def next_node(current_node):
    input_element = current_node.element
    
    ## 第一种情况
    if current_node.rightNode != None:
        current_node = current_node.rightNode
        while current_node.leftNode != None:
            current_node = current_node.leftNode
        else:
            print(input_element, '在中序遍历序列中的下一个节点是：', current_node.element)
            
    ## 第二种情况
    elif current_node.rightNode == None and current_node is current_node.parentNode.leftNode:
        print(input_element, '在中序遍历序列中的下一个节点是：', current_node.parentNode.element)
    
    ## 第三种情况
    elif current_node.rightNode == None and current_node is current_node.parentNode.rightNode:
        current_node = current_node.parentNode
        while not (current_node is current_node.parentNode.leftNode):
            current_node = current_node.parentNode
        else:
            print(input_element, '在中序遍历序列中的下一个节点是：', current_node.parentNode.element)
    

current_node = node.leftNode
print('中序遍历序列', middle_list)
next_node(current_node)
```

中序遍历序列 ['d', 'b', 'h', 'e', 'i', 'a', 'f', 'c', 'g']

b 在中序遍历序列中的下一个节点是： h

**Inverview-8测试用例**

```python
print('中序遍历序列', middle_list)

## 节点是没有右子树，但它是父节点的左子节点
current_node = node.leftNode.leftNode
next_node(current_node)

## 节点是没有右子树，但它是父节点的右子节点
current_node = node.leftNode.rightNode.rightNode
next_node(current_node)
```

中序遍历序列 ['d', 'b', 'h', 'e', 'i', 'a', 'f', 'c', 'g']

d 在中序遍历序列中的下一个节点是： b

i 在中序遍历序列中的下一个节点是： a

> 作者：[@mantchs](https://github.com/NLP-LOVE/ML-NLP)
>
> GitHub：[https://github.com/NLP-LOVE/CodingInterviews2-ByPython](https://github.com/NLP-LOVE/CodingInterviews2-ByPython)
>
> 有意向一起完成此项目或者有问题、有补充的可以加入《剑指offer》讨论群【818185620】<a target="_blank" href="//shang.qq.com/wpa/qunwpa?idkey=8c188e86e0eac4a214861c2c706a9c0baf75176e16e52f07b8a64d1a13f99a0d"><img border="0" src="http://pub.idqqimg.com/wpa/images/group.png" alt="《剑指offer》讨论群" title="《剑指offer》讨论群"></a>
