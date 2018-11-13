# 用栈实现队列
## 要求

    使用栈实现队列的下列操作：
    
    push(x) -- 将一个元素放入队列的尾部。
    pop() -- 从队列首部移除元素。
    peek() -- 返回队列首部的元素。
    empty() -- 返回队列是否为空。

## 示例

    MyQueue queue = new MyQueue();

    queue.push(1);
    queue.push(2);  
    queue.peek();  // 返回 1
    queue.pop();   // 返回 1
    queue.empty(); // 返回 false
    
## 思路
  
    建立两个栈，入栈时进入栈1，出栈时，判断栈2是否为空，若空，将栈1元素全部倒入栈2，然后pop栈2顶，如果栈2不为空，直接pop栈2顶。

## Python代码

```python
class MyQueue:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.stack1 = []
        self.stack2 = []

        

    def push(self, x):
        """
        Push element x to the back of queue.
        :type x: int
        :rtype: void
        """
        self.stack1.append(x)
        return

    def pop(self):
        """
        Removes the element from in front of queue and returns that element.
        :rtype: int
        """
        if self.stack2 == []:
            while self.stack1 != []:
                a = self.stack1.pop()
                self.stack2.append(a)
        m = self.stack2.pop()
        return m
        
        

    def peek(self):
        """
        Get the front element.
        :rtype: int
        """
        if self.stack2 == []:
            while self.stack1 != []:
                a = self.stack1.pop()
                self.stack2.append(a)
        n = self.stack2[-1]
        return n
        
        

    def empty(self):
        """
        Returns whether the queue is empty.
        :rtype: bool
        """
        if self.stack1 == [] and self.stack2 == []:
            return True
        else:
            return False
        


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```

## C++代码

```c
class MyQueue {
public:
    /** Initialize your data structure here. */
   stack<int> s1, s2;
    
    /** Push element x to the back of queue. */
    void push(int x) {
        s1.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
       if(s2.empty()){
           while(!s1.empty()){
               s2.push(s1.top());
               s1.pop();
           }
       }
        int a = s2.top();
        s2.pop();
        return a;
    }
    
    /** Get the front element. */
    int peek() {
        if(s2.empty()){
           while(!s1.empty()){
               s2.push(s1.top());
               s1.pop();
           }
       }
        return s2.top();
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        if(s1.empty() && s2.empty())
            return true;
        return false;
    }
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * bool param_4 = obj.empty();
 */
```