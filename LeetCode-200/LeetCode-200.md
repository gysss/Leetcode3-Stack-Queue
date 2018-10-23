# 岛屿的个数

## 要求

* 给定一个由 `'1'`（陆地）和 `'0'`（水）组成的的二维网格，计算岛屿的数量。一个岛被水包围，并且它是通过水平方向或垂直方向上相邻的陆地连接而成的。你可以假设网格的四个边均被水包围。

## 示例
* 输入:
    11110
    11010
    11000
    00000
* 输出:1
* 输入:
    11000
    11000
    00100
    00011
* 输出: 3

## 思路
* 遍历，若为1，将其上下左右为1的全部置为0，ans+1，遍历完，返回ans

## Python代码

```python
class Solution:
    _landform = []
    _row = 0
    _col = 0
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        self._landform = []
        self._row = len(grid)
        if self._row == 0:
            return 0
        for s in grid:
            l = list(s)
            self._landform.append(l)
        self._col = len(grid[0]) 
        ans = 0
        for i in range(self._row):
            for j in range(self._col):
                if self._landform[i][j] == '1':
                    ans+=1
                    self.explore(i, j)
        return ans
    
    def explore(self, x, y):
        if x>=0 and y>=0 and x<self._row and y<self._col and self._landform[x][y] == '1':
            self._landform[x][y] = '0'
            self.explore(x-1, y)
            self.explore(x, y-1)
            self.explore(x+1, y)
            self.explore(x, y+1)
```