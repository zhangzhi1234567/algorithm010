# leetcode_153. 寻找旋转排序数组中的最小值

二分查找
假设按照升序排序的数组在预先未知的某个点上进行了旋转。
( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。
请找出其中最小的元素。
你可以假设数组中不存在重复元素。
[链接](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)


### Binary search

---

1.中间数和左边界
当nums[mid] < nums[left]，能否确定最小值在左侧？——可以，此时说明区间[left...mid]出现了降序
当nums[mid] > nums[left]，能否确定最小值在右侧？——不能，如果右边无序，则在右边，如果右边有序则在左边
2.中间数和右边界
00000123
当nums[mid] < nums[right]，能否确定最小值在左侧？——可以，此时说明区间[mid...right]保持升序
当nums[mid] > nums[right]，能否确定最小值在右侧？——可以，此时说明区间[mid...right]出现了降序

- **golang**
```go
/*
0. 从中点分成两段，结果肯定在无序的一边。当没有拐点时，肯定在中点左边。
1. 通过nums[mid]和最右边值比较，就可以知道那一表示无序的
2. 继续二分查找，知道循环退出时，即找到结果 //我们一直在删去不可能存在最小值的区间，当区间只剩下一个元素，那么它一定是最小值。
*/
func findMin(nums []int) int {
    left := 0
    right := len(nums) - 1
    for left < right {        //不能有等号，循环退出时去left
        mid := (left + right) >> 1
        if nums[mid] > nums[right] { //左边是有序的,且mid一定不是最大值，进去无序一遍继续找
            left = mid + 1   //mid一定不是最小值
        }else {              //右边有序，
            right = mid      //nums[mid] <= nums[right] , mid可能是最小值
        }
    }
    return nums[left]
}
```
