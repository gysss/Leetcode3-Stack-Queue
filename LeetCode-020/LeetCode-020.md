## 要求
* 给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。
  有效字符串需满足：
    左括号必须用相同类型的右括号闭合。
    左括号必须以正确的顺序闭合。
    注意空字符串可被认为是有效字符串。

## 示例
  * 输入: "()[]{}"
    输出: true
  * 输入: "(]"
    输出: false

## 思路
  * 建栈存入左符号，有右符号时退栈最上面元素，最后判断栈是否为空，空则True

## Python代码

```python
class Solution:
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        stack_top = -1
        left_symbol = ['{', '(', '[']
        my_dict = {'}':'{', ')':'(', ']':'['}
        if s == None:
            return True
        for i in s:
            if i in left_symbol:
                stack.append(i)
                stack_top+=1
            elif i in my_dict:
                if stack_top>=0 and stack[stack_top] == my_dict[i]:
                    stack.pop()
                    stack_top -= 1
                else:
                    return False
        if stack_top == -1:
            return True
        else:
            return False
```

## C++代码

```c
class Solution {
public:
    bool isValid(string s) {
        stack<char> t;
        for(int i = 0; i< s.length(); i++){
            if(s[i] == '(' || s[i] == '{' || s[i] == '['){
                t.push(s[i]);
            }
            else if(s[i] == ')'){
                if(i == 0 || t.empty() || t.top()!= '(' )
                    return false;
                t.pop();
            }
             else if(s[i] == '}'){
                if(i == 0 || t.empty() || t.top() != '{' )
                    return false;
                t.pop();
            }
             else if(s[i] == ']'){
                if(i == 0  || t.empty() || t.top() != '[')
                    return false;
                t.pop();
            }
        }
        return t.empty();
    }
};
```