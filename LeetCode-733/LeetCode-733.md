## 图像渲染
### 要求
* 有一幅以二维整数数组表示的图画，每一个整数表示该图画的像素值大小，数值在 0 到 65535 之间。
给你一个坐标 (sr, sc) 表示图像渲染开始的像素值（行 ，列）和一个新的颜色值 newColor，让你重新上色这幅图像。
为了完成上色工作，从初始坐标开始，记录初始坐标的上下左右四个方向上像素值与初始坐标相同的相连像素点，接着再记录这四个方向上符合条件的像素点与他们对应四个方向上像素值与初始坐标相同的相连像素点，……，重复该过程。将所有有记录的像素点的颜色值改为新的颜色值。
最后返回经过上色渲染后的图像。

### 示例
*
    输入: 
    image = [[1,1,1],[1,1,0],[1,0,1]]
    sr = 1, sc = 1, newColor = 2
    输出: [[2,2,2],[2,2,0],[2,0,1]]
    解析: 
    在图像的正中间，(坐标(sr,sc)=(1,1)),
    在路径上所有符合条件的像素点的颜色都被更改成2。
    注意，右下角的像素没有更改为2，
    因为它不是在上下左右四个方向上与初始点相连的像素点。

### 思路
* 建立一个函数来获取输入坐标的四个方向的坐标，要求这四个坐标在范围内，且值不等于newColor
* 从给定的第一个位置开始转变颜色，调用函数来获取位置， 建立一个队列来保存位置，从队列头开始判断是否需要变色，若变色，则调用函数添加新的位置到队列中，如此反复，到队列为空停止

### Python代码

```python
class Solution:
    def floodFill(self, image, sr, sc, newColor):
        """
        :type image: List[List[int]]
        :type sr: int
        :type sc: int
        :type newColor: int
        :rtype: List[List[int]]
        """
        stack = []
        length = len(image) # 图片长
        width = len(image[0]) # 图片的宽
        
        def four_dictions(image, x, y):
            """
            四个方向的元素
            return：List[List[int]]
            """
            list_to_add = []
            if  (x-1)>=0 and image[x-1][y] != newColor:
                list_to_add.append([x-1,y])
            if (y-1)>=0  and image[x][y-1] != newColor:
                list_to_add.append([x,y-1])
            if  (x+1) < length and image[x+1][y] != newColor:
                list_to_add.append([x+1,y])
            if  (y+1) < width and image[x][y+1] != newColor:
                list_to_add.append([x,y+1])
            return list_to_add
        
        a = image[sr][sc]
        image[sr][sc] = newColor
        stack = stack + four_dictions (image, sr, sc)
        while stack != []:
            x = stack[0][0]
            y = stack[0][1]
            if image[x][y] == a:
                stack = stack + four_dictions (image, x, y)
                image[x][y] = newColor
            del stack[0]
        return image
```