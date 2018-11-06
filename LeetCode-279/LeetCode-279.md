# 完全平方数

## 要求
*给定正整数 n，找到若干个完全平方数（比如 1, 4, 9, 16, ...）使得它们的和等于 n。你需要让组成和的完全平方数的个数最少。

## 示例
* 输入
  n = 12
* 输出
  3
* 解释
  12 = 4 + 4 + 4

## 思路
  * dp状态转移公式：dp[i] = min(dp[i], dp[i - j * j] + 1)

## 代码实现

```c
class Solution {
public:
    int numSquares(int n) {
        vector<int> dp(n+1);
        dp[1] = 1;
        for(int i = 2; i <= n; i++) {
            int temp = 99999999;
            for(int j = 1; j * j <= i; j++) {
                if(j * j == i) {
                    temp = 1;
                    break;
                }
                temp = min(temp, dp[i-j*j] + 1);
            }
            dp[i] = temp;
        }
        return dp[n];
    }
};
```