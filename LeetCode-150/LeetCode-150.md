# 逆波兰表达式求值
## 要求
* 根据逆波兰表示法，求表达式的值。
  有效的运算符包括+，-，*，/。每个运算对象可以是整数，也可以是另一个逆波兰表达式。
说明：
整数除法只保留整数部分。
给定逆波兰表达式总是有效的。换句话说，表达式总会得出有效数值且不存在除数为 0 的情况。

## 示例
* 输入: ["2", "1", "+", "3", "*"]
* 输出: 9
* 解释: ((2 + 1) * 3) = 9

## 思路
* 思路其实很简单，就是建栈，遇到符号退出两个数进行计算，然后再进栈,注意‘/’的计算，不能得到-0

## python代码

```python
class Solution:
    def evalRPN(self, tokens):
        """
        :type tokens: List[str]
        :rtype: int
        """
        labels = ['+', '-', '*', '/']
        my_stack = []
        index = -1
        for i in tokens:
            if i not in labels:
                my_stack.append(i)
                index += 1
            else:
                a = eval(my_stack.pop())
                b = eval(my_stack.pop())
                index -= 2
                if i == '+':
                    c = str(a + b)
                    my_stack.append(c)
                    index += 1
                elif i == '-':
                    c = str(b-a)
                    my_stack.append(c)
                    index += 1
                elif i == '*':
                    c = str(a * b)
                    my_stack.append(c)
                    index += 1
                elif i == '/':
                    c = str(int(b/a))
                    my_stack.append(c)
                    index += 1
        return eval(my_stack[index])
```