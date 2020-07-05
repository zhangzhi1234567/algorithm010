# leetcode_74. 搜索二维矩阵

二分查找
编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：
每行中的整数从左到右按升序排列。
每行的第一个整数大于前一行的最后一个整数。
[题目链接](https://leetcode-cn.com/problems/search-a-2d-matrix/)
示例 1:
```
输入:
matrix = [
 [1,   3,  5,  7],
 [10, 11, 16, 20],
 [23, 30, 34, 50]
]
target = 3
输出: true
```
### Binary Search

   1.    两次二分查找，先用二分查找目标所在行，然后在所在行中继续二分
   1. 注意查找所在行[up, down]时，用本行中最后的值和target比较
      1. target > nums[mid]时，在（mid, down]区间， 左开又闭
      1. target < nums[mid] 时，相反在[up, mid] 闭区间，因为可能在本行，所以Mid侧为闭区间
- **golang**
```go
func searchMatrix(matrix [][]int, target int) bool {
    if len(matrix) == 0 {
        return false
    }
    col := len(matrix[0]) //列
    row := len(matrix)    //行
    up := 0               
    down := row - 1
    var mid int
    for up < down {       //二分查找所在行
        mid = up + ((down - up) >> 1)
        if target > matrix[mid][col-1] { //目标比中间值大，则移上边界 (mid, down]
            up = mid + 1
        }else {          //目标比中间值小结果在[up, mid]之间
            down = mid   //不能减一，可能在本行
        }   
    }                   //最终up和down在同一行
    left := 0
    right := col - 1
    for left <= right {
        mid := left + ((right - left) >> 1)
        if target == matrix[up][mid] {
            return true
        }
        if target < matrix[up][mid] {
            right = mid - 1
        }else {
            left = mid + 1
        }
    }
    return false
}
```


