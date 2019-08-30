## Inverview6：从尾到头打印链表

**题目**：输入一个链表的头节点，从尾到头反过来打印出每个节点的值。链表节点定义如下:

1. 创建链表类。
2. 链表的头部是最新的节点，所以要从尾部开始输出链表，必需要借助于栈，因为栈基于后进先出的原则，符合从尾到头打印链表，所以要创建一个栈类，存放栈数据。
3. 链表从头部开始压数据入栈，再使用栈类进行出栈操作。

**链表的时间复杂度：O(n)，数组的查询时间复杂度为：O(1)**

```python

## 栈的实现  后进先出
class Stack():
    def __init__(self):
        self.stack = []
        self.top = -1
    
    def push(self, x): # 入栈之前检查是否满了
        self.stack.append(x)
        self.top += 1
    
    def pop(self): # 出栈之前检查是否为空
        if self.isempty():
            return None
        else:
            self.top = self.top - 1
            return self.stack[self.top + 1]
    
    def isempty(self):
        return self.top == -1
    
    def showstack(self):
        print(self.stack)


## 链表
class Node():
    
    def __init__(self, data, next = None):
        self.data = data
        self.next = next

## 创建链表
head = None
for i in range(10):
    head = Node(i, head)

## 链表入栈
probe = head
stack = Stack()
while probe != None:
    stack.push(probe.data)
    probe = probe.next

## 链表出栈
while True:
    stack_data = stack.pop()
    if stack_data == None:
        break
    else:
        print(stack_data, end=',')
```

0,1,2,3,4,5,6,7,8,9,

**Inverview6测试用例**

```python
## 输入的链表是None
head = Node(None, None)

## 链表入栈
probe = head
stack = Stack()
while probe != None:
    stack.push(probe.data)
    probe = probe.next

## 链表出栈
while True:
    stack_data = stack.pop()
    if stack_data == None:
        break
    else:
        print(stack_data, end=',')
```

------

> 作者：[@mantchs](https://github.com/NLP-LOVE/ML-NLP)
>
> GitHub：[https://github.com/NLP-LOVE/CodingInterviews2-ByPython](https://github.com/NLP-LOVE/CodingInterviews2-ByPython)
>
> 有意向一起完成此项目或者有问题、有补充的可以加入《剑指offer》讨论群【818185620】<a target="_blank" href="//shang.qq.com/wpa/qunwpa?idkey=8c188e86e0eac4a214861c2c706a9c0baf75176e16e52f07b8a64d1a13f99a0d"><img border="0" src="http://pub.idqqimg.com/wpa/images/group.png" alt="《剑指offer》讨论群" title="《剑指offer》讨论群"></a>
