# 用队列实现栈
## 要求

    使用队列实现栈的下列操作：
    
    push(x) -- 元素 x 入栈
    pop() -- 移除栈顶元素
    top() -- 获取栈顶元素
    empty() -- 返回栈是否为空

## 思路
    建立两个队列，进栈时哪个队列不为空进哪个，出栈时，将一个队列中的元素全部进到另一个队列中，并弹出最后一个。
    
## python代码

```python
class MyStack:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.stack1 = []
        self.stack2 = []


    def push(self, x):
        """
        Push element x onto stack.
        :type x: int
        :rtype: void
        """
        if self.stack2 == []:
            self.stack1.append(x)           
        else:
            self.stack2.append(x)
        
    def pop(self):
        """
        Removes the element on top of the stack and returns that element.
        :rtype: int
        """
        if self.stack1 != []:
            self.stack1.reverse()
            while(self.stack1 != []):
                self.stack2.append(self.stack1.pop())
            m = self.stack2.pop()
        else:
            self.stack2.reverse()
            while(self.stack2 != []):
                self.stack1.append(self.stack2.pop())
            m = self.stack1.pop()
        return m
        
    def top(self):
        """
        Get the top element.
        :rtype: int
        """
        if self.stack1 != []:
            self.stack1.reverse()
            while(self.stack1 != []):
                self.stack2.append(self.stack1.pop())
            m = self.stack2[-1]
        else:
            self.stack2.reverse()
            while(self.stack2 != []):
                self.stack1.append(self.stack2.pop())
            m = self.stack1[-1]
        return m

    def empty(self):
        """
        Returns whether the stack is empty.
        :rtype: bool
        """
        if self.stack1 == [] and self.stack2 == []:
            return True
        else:
            return False


# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```