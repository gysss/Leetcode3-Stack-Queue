# 字符串解码
## 要求
* 给定一个经过编码的字符串，返回它解码后的字符串。
编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。
你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。
此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

##示例
* s = "3[a]2[bc]", 返回 "aaabcbc".
s = "3[a2[c]]", 返回 "accaccacc".
s = "2[abc]3[cd]ef", 返回 "abcabccdcdcdef".

## 思路
* 建立两个栈，n_stack保存的是重复的数目，i_stack保存的是遇到'['时的string下标，这样当又遇到‘]'时，弹出重复数目n和下标i，将string下标i到当前结尾处的字符复制即可

## python代码

```python
class Solution:
    def decodeString(self, s):
        """
        :type s: str
        :rtype: str
        """
        n_stack = []
        i_stack = []
        string = ''
        i = 0
        n = 0
        
        for c in s:
            if '0' <= c <= '9':
                n = n * 10 + int(c)
            elif c == '[' :
               i_stack.append(i)
               n_stack.append(n-1) # n-1是因为本身已经加入到string一次了，所以再重复n-1次即可
               n = 0
            elif c == ']':
                string = string + string[i_stack.pop():len(string)] * n_stack.pop()
                i = len(string)
            else:
                string += c
                i += 1
                
        return string
```