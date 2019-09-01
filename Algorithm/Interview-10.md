## Inverview10-1：斐波那契数列

**题目**：写一个函数，输入n,求斐波那契( Fibonacci)数列的第n项。斐波那契数列公式如下：

![](https://gitee.com/kkweishe/images/raw/master/ML/2019-9-1_10-43-12.png)

递归虽然有简洁的优点，但它同时也有显著的**缺点**。递归由于是函数调用自身，而函数调用是有时间和空间的消耗的:每一次函数调用，都需要在内存栈中分配空间以保存参数、返回地址及临时变量，而且往栈里压入数据和弹出数据都需要时间。这就不难理解上述的例子中递归实现的效率不如循环。也有可能会栈溢出。

我们不难发现，在这棵树中有很多节点是重复的，而且重复的节点数会随着 n 的增大而急剧增加，这意味着计算量会随着 n 的增大而急剧增大。事实上，用递归方法计算的时间复杂度是以 n 的指数的方式递增的。读者不妨求斐波那契数列的第100项试试，感受一下这样递归会慢到什么程度。

![](https://gitee.com/kkweishe/images/raw/master/ML/2019-9-1_10-46-46.png)

```python
def Fibonacci(n):
    
    if n < 0:
        return None
    else:
        f_value = [0, 1]
        if n in [0, 1]:
            return f_value[n]
        else:
            for i in range(2, n + 1):
                f_value[i % 2] = f_value[0] + f_value[1]
            
            return f_value[n % 2]
            

Fibonacci(10)
```

55

## Inverview10-2：青蛙跳台阶问题

**题目**：一只青蛙一次可以跳上 1 级台阶，也可以跳上 2 级台阶。求该青蛙跳上一个 n级的台阶总共有多少种跳法。

首先我们考虑最简单的情况。如果只有 1 级台阶，那显然只有一种跳法。如果有 2 级台阶，那就有两种跳法: 一种是分两次跳，每次跳 1 级;另一种就是一次跳 2 级。

接着我们再来讨论一般情况。我们把 n 级台阶时的跳法看成 n 的函数,记为 f(n)。当 n>2 时，第一次跳的时候就有两种不同的选择:一是第一次只跳 1 级，此时跳法数目等于后面剩下的 n-1 级台阶的跳法数目，即为 f(n- 1);二是第一次跳 2 级，此时跳法数目等于后面剩下的 n -2 级台阶的跳法数目，即为 f(n-2)。**因此，n 级台阶的不同跳法的总数 f(n)=f(n- 1)+f(n -2) 。分析到这里，我们不难看出这实际上就是斐波那契数列了。**

> 作者：[@mantchs](https://github.com/NLP-LOVE/ML-NLP)
>
> GitHub：[https://github.com/NLP-LOVE/CodingInterviews2-ByPython](https://github.com/NLP-LOVE/CodingInterviews2-ByPython)
>
> 有意向一起完成此项目或者有问题、有补充的可以加入《剑指offer》讨论群【818185620】<a target="_blank" href="//shang.qq.com/wpa/qunwpa?idkey=8c188e86e0eac4a214861c2c706a9c0baf75176e16e52f07b8a64d1a13f99a0d"><img border="0" src="http://pub.idqqimg.com/wpa/images/group.png" alt="《剑指offer》讨论群" title="《剑指offer》讨论群"></a>
