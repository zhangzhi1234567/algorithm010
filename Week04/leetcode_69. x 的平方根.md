# leetcode_69. x 的平方根

实现  int sqrt(int x)  函数。
计算并返回  x  的平方根，其中  x 是非负整数。
由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。
示例 1:      示例 2:
输入: 4      输入: 8
输出: 2      输出: 2
### golang

---

- 二分查找
```go
func mySqrt(x int) int {
//因为结果在[0,x/2 + 1]之间，这个函数是单调递增，可用二分查找
    left := 1
    right := x/2 + 1
    for left <= right {
    mid := (left + right) >> 1 // >>1比/2效率高很多 //防止left+right越界 可以优化成left + (right - left)>>1
        if x == mid * mid {
            return mid
        }else if x > mid * mid {
            left = mid + 1
        }else {
            right = mid - 1
        }
    }
    return right  //退出循环的条件是左右指针不再形成区间，这时的结果肯定在p[right, left]之间，取整就是right
}
```

---



