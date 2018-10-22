# 设计队列
## 要求
* 设计你的循环队列

## 示例
* MyCircularQueue circularQueue = new MycircularQueue(3); // 设置长度为3
  circularQueue.enQueue(1);  // 返回true
  circularQueue.enQueue(2);  // 返回true
  circularQueue.enQueue(3);  // 返回true
  circularQueue.enQueue(4);  // 返回false,队列已满
  circularQueue.Rear();  // 返回3
  circularQueue.isFull();  // 返回true
  circularQueue.deQueue();  // 返回true
  circularQueue.enQueue(4);  // 返回true
  circularQueue.Rear();  // 返回4

## Python代码

```python
class MyCircularQueue(object):

    def __init__(self, k):
        """
        Initialize your data structure here. Set the size of the queue to be k.
        :type k: int
        """
        self.queue = [None] * k
        self.size = k
        self.front = 0
        self.rear = 0

    def enQueue(self, value):
        """
        Insert an element into the circular queue. Return true if the operation is successful.
        :type value: int
        :rtype: bool
        """
        if self.isFull():
            return False
        if self.rear == (self.size-1):
            self.queue[self.rear] = value
            self.rear = 0
        else:
            self.queue[self.rear] = value
            self.rear+=1
        return True
    
    def deQueue(self):
        """
        Delete an element from the circular queue. Return true if the operation is successful.
        :rtype: bool
        """
        if self.isEmpty():
            return False
        self.queue[self.front] = None
        if self.front == (self.size-1):
            self.front = 0
        else:
            self.front += 1
        return True
        

    def Front(self):
        """
        Get the front item from the queue.
        :rtype: int
        """
        if self.isEmpty():
            return -1
        return self.queue[self.front]
        

    def Rear(self):
        """
        Get the last item from the queue.
        :rtype: int
        """
        if self.isEmpty():
            return -1
        if self.rear == 0:
            return self.queue[self.size-1]
        else:
            return self.queue[self.rear-1]

    def isEmpty(self):
        """
        Checks whether the circular queue is empty or not.
        :rtype: bool
        """
        if (self.rear == self.front) and (self.queue[self.rear] == None):
            return True
        else:
            return False
        

    def isFull(self):
        """
        Checks whether the circular queue is full or not.
        :rtype: bool
        """
        if self.rear == self.front and self.queue[self.rear] is not None:
            return True
        else:
            return False


# Your MyCircularQueue object will be instantiated and called as such:
# obj = MyCircularQueue(k)
# param_1 = obj.enQueue(value)
# param_2 = obj.deQueue()
# param_3 = obj.Front()
# param_4 = obj.Rear()
# param_5 = obj.isEmpty()
# param_6 = obj.isFull()
```