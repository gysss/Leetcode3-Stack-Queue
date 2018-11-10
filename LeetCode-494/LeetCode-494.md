# 目标和
## 要求
    给定一个非负整数数组，a1, a2, ..., an, 和一个目标数，S。现在你有两个符号 + 和 -。对于数组中的任意一个整数，你都可以从 + 或 -中选择一个符号添加在前面。返回可以使最终数组和为目标数 S 的所有添加符号的方法数。
## 示例
    输入: nums: [1, 1, 1, 1, 1], S: 3
    输出: 5
    解释: 
    
    -1+1+1+1+1 = 3
    +1-1+1+1+1 = 3
    +1+1-1+1+1 = 3
    +1+1+1-1+1 = 3
    +1+1+1+1-1 = 3
    
    一共有5种方法让最终目标和为3。
    
## 思路
    深度优先搜索，当cnt和nums大小相等时，判断sum和S是否相等，若相等，则result+1，结果返回result
    
## C++代码

```c
class Solution {
public:
    int result;
    
    int findTargetSumWays(vector<int>& nums, int S) {
        dfs(0, 0, nums, S);
        return result;
    }
    void dfs(int sum, int cnt, vector<int>& nums, int S){
        if(cnt == nums.size()){
            if(sum == S)
                result++;
            return;
        }
        dfs(sum + nums[cnt], cnt+1, nums, S);
        dfs(sum - nums[cnt], cnt+1, nums, S);
    }
};
```