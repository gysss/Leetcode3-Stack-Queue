# 每日温度
## 要求
* 根据每日 气温 列表，请重新生成一个列表，对应位置的输入是你需要再等待多久温度才会升高的天数。如果之后都不会升高，请输入 0 来代替。

## 示例
* 例如，给定一个列表 temperatures = [73, 74, 75, 71, 69, 72, 76, 73]，你的输出应该是 [1, 1, 4, 2, 1, 1, 0, 0]。

## 思路
建立一个栈，首先一个温度进栈，如果下一个大于他，则出战，返回两个温度序号差值，如果小于他，则也进栈，栈内存放的是温度的序号

## Python代码

```python
class Solution:
    def dailyTemperatures(self, temperatures):
        """
        :type temperatures: List[int]
        :rtype: List[int]
        """
        tem_Stack = []
        index = -1
        length = len(temperatures)
        waitDays = [0] * (length)
        for i in range(length):
            if index == -1:
                tem_Stack.append(i)
                index += 1
            else:
                while(True):
                    if index == -1:
                        tem_Stack.append(i)
                        index += 1
                        break
                    else:
                        t = tem_Stack[index]
                        if  temperatures[i] <= temperatures[t]:
                            tem_Stack.append(i)
                            index += 1
                            break
                        else:
                            tem_Stack.pop()
                            index -= 1
                            waitDays[t] = i - t
        return waitDays
```