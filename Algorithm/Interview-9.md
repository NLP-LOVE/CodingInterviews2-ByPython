## Inverview-9：用两个栈实现队列

**题目**：用两个栈实现一个队列。队列的声明如下，请实现它的两个函数appendTail和deleteHead,分别完成在队列尾部插入节点和在队列头部删除节点的功能。

1. 创建一个栈类。
2. 创建一个队列类，该队列类包含两个栈stack1和stack2，当需要添加元素到队列时，其实就是往stack1中入栈。
3. 如果是要消费队列时，需要先判断stack2是否为空，如果为空，那么就把stack1中的数据逐个出栈并对stack2入栈，这样就使得先进来的数据在stack2的栈顶，实现了队列的先进先出原则；如果不为空，那么stack2直接出栈。

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
            pop_value = self.stack[self.top + 1]
            del self.stack[self.top + 1]
            return pop_value
    
    def isempty(self):
        return self.top == -1
    
    def showstack(self):
        print(self.stack)
    
    def get_deep(self):
        return self.top + 1

## 两个栈实现一个队列
class Queue():
    def __init__(self):
        self.stack_one = Stack()
        self.stack_two = Stack()
        self.deep = 0
    
    ## 向队列添加数据
    def append(self, x):
        self.stack_one.push(x)
        self.deep += 1
    
    ## 取出队列的数据
    def get_head(self):
        if self.isempty():
            return None
        elif self.stack_two.isempty():
            while not self.stack_one.isempty():
                self.stack_two.push(self.stack_one.pop())
        
        self.deep = self.deep - 1
        return self.stack_two.pop()
            
    
    def isempty(self):
        return self.deep == 0

queue = Queue()
queue.append('a')
queue.append('b')
queue.append('c')
print(queue.get_head())
print(queue.get_head())

queue.append('d')
print(queue.get_head())
print(queue.get_head())
```

a

b

c

d

**Inverview-9测试用例**

```python
## 往空队列里添加元素和删除元素
queue = Queue()
queue.append('a')
print(queue.get_head())
print(queue.get_head())
```

a

None

> 作者：[@mantchs](https://github.com/NLP-LOVE/ML-NLP)
>
> GitHub：[https://github.com/NLP-LOVE/CodingInterviews2-ByPython](https://github.com/NLP-LOVE/CodingInterviews2-ByPython)
>
> 有意向一起完成此项目或者有问题、有补充的可以加入《剑指offer》讨论群【818185620】<a target="_blank" href="//shang.qq.com/wpa/qunwpa?idkey=8c188e86e0eac4a214861c2c706a9c0baf75176e16e52f07b8a64d1a13f99a0d"><img border="0" src="http://pub.idqqimg.com/wpa/images/group.png" alt="《剑指offer》讨论群" title="《剑指offer》讨论群"></a>
