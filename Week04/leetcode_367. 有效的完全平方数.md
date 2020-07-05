# leetcode_367. 有效的完全平方数

给定一个正整数 num，编写一个函数，如果 num 是一个完全平方数，则返回 True，否则返回 False。
说明：不要使用任何内置的库函数，如   sqrt。
示例 1：
输入：16
输出：True
### golang

---

- 二分查找
满足二分查找的条件，所以可以用二分查找，直接套公式即可
```go
func isPerfectSquare(num int) bool {
    left := 0
    right := num/2 + 1
    for left <= right {
        mid := (left + right) >> 1
        if mid * mid == num {
            return true
        }else if mid * mid < num {
            left = mid + 1
        }else {
            right = mid - 1
        }
    }
    return false
}
```

---



