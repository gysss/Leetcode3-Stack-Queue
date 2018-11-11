# 二叉树的中序遍历
## 要求
    给定一个二叉树，返回它的中序遍历。

## 进阶
    递归算法很简单，能否用迭代完成

## 递归算法
### C++代码

```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> result;
    vector<int> inorderTraversal(TreeNode* root) {
        dfs(root);
        return result;
    }
    void dfs(TreeNode* root){
        if(root == NULL)
            return;
        dfs(root->left);
        result.push_back(root->val);
        dfs(root->right);
    }
};
```

### Python代码

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        res = []
        if root is None:
            return res
        res.extend(self.inorderTraversal(root.left))
        res.append(root.val)
        res.extend(self.inorderTraversal(root.right))
        return res
```