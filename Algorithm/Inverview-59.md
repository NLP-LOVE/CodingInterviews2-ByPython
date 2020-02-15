## Inverview59-2：队列的最大值

**题目**：请定义一个队列并实现函数 max 得到队列里的最大值，要求函数 max、push_back 和 pop_front 的时间复杂度都是 O(1)。也就是对以下函数进行填充并满足要求。

```python
class MaxQueue:

    def __init__(self):
        

    def max_value(self) -> int:
        

    def push_back(self, value: int) -> None:
        

    def pop_front(self) -> int:
```

例如输入，第一个列表表示调用函数的顺序，第二列表示调用函数时所带的参数:

```
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
```

输出为:

```
[null,null,null,2,1,2]
```



**解题思路**

- 定义两个队列，A 队列存放的是输入的队列，B 队列存放的是可能的最大值队列。
- 例如输入 [2,3,1,2,6,2,5,1] 队列，首先先输入个 2，那么 A 队列里就有 2，B 队列里也是2。
- 然后是输入 3，A 队列就有 [2,3]，B 队列里的 2 比 3 小，所以就要把 B 队列清空并赋值 3。
- 接下来输入 1，A = [2,3,1]，B队列就要考虑了，因为 1 比 3 小，说明当 A 队列里的 3 出队列之后，后面的 1 有可能是最大值，所以我们要把 1 加入到 B 队列里，接下来依次进行，会发现 B 队列永远都是按照从大到小排序好的。
- 所以，当我们需要 pop_front A队列的时候，就需要比较 A 队列里的第一个元素和 B 队列里的第一个元素，如果相等，删除 B 队列里的头部元素。

**以下代码可提交至LeetCode：**

[https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

```python
class MaxQueue:

    def __init__(self):
        self.queue = []       # 输入队列
        self.max_queue = []   # 可能最大值队列

    def max_value(self) -> int:
        if len(self.queue) == 0:
            return -1
        return self.max_queue[0]

    def push_back(self, value: int) -> None:
        self.queue.append(value)

        ## 判断是否要删除 最大值 队列
        if len(self.max_queue) == 0:
            self.max_queue.append(value)
        else:
            while len(self.max_queue) != 0 and self.max_queue[-1] < value:
                self.max_queue.pop()
            self.max_queue.append(value)

        return None

    def pop_front(self) -> int:
        if len(self.queue) == 0:
            return -1

        queue_front = self.queue[0]

        ## 判断头部元素是否相等
        if queue_front == self.max_queue[0]:
            del self.max_queue[0]

        del self.queue[0]
        return queue_front

# 以下是调用函数
input_behavior = ["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
input_num = [[],[1],[2],[],[],[]]
result = []

for i, behavior in enumerate(input_behavior):

    if behavior == 'MaxQueue':
        maxQueue = MaxQueue()
        result.append(None)

    if behavior == 'push_back':
        result.append(maxQueue.push_back(input_num[i][0]))

    if behavior == 'max_value':
        result.append(maxQueue.max_value())

    if behavior == 'pop_front':
        result.append(maxQueue.pop_front())

print(result)
```

结果如下:

```
[None, None, None, 2, 1, 2]
```



![](https://gitee.com/kkweishe/images1/raw/master/ML/2020-2-14_10-42-38.png)
