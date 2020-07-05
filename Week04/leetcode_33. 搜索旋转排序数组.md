# leetcode_33. 搜索旋转排序数组

leetcode二分查找 
假设按照升序排序的数组在预先未知的某个点上进行了旋转。
( 例如，数组  [0,1,2,4,5,6,7]  可能变为  [4,5,6,7,0,1,2]  )。
搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回  -1  。
你可以假设数组中不存在重复的元素。
你的算法时间复杂度必须是  O(log  n) 级别。
```
输入: nums = [4,5,6,7,0,1,2], target = 0
输出: 4
```
### golang

---

- **直接二分查找**

0.target必然是在有序的一侧
1.先根据中点值 判断是中点左边有序，还是中点右边有序
2.在判断目标值是在有序的一遍还是在无序的一边
3.在有序的一遍则继续二分查找即可， 在无序的一遍，则进行归约，继续以上步骤
```go
func search(nums []int, target int) int {
    if len(nums) == 0 {
        return -1
    }
    left := 0
    right := len(nums) - 1
    for left <= right {
        mid := left + ((right - left) >> 1)
        if target == nums[mid] {
            return mid
        }
        if nums[mid] >= nums[0] { //中点左边有序 =号考虑到只有两个数时的情况，如果没有旋转，且目标在最右边，则一直左边有序，直到归约到nums[left]==target
            if target >= nums[0] && target < nums[mid] { //目标在有序的这里
                right = mid - 1
            }else {
                left = mid + 1   //目标不在有序的一遍，继续规约查找
            }
        }else { //中点右边有序
            if target > nums[mid] && target <= nums[right] {
                left = mid + 1
            }else {
                right = mid -1   //目标不在有序的一遍，继续规约查找
            }
        }
    }
    return -1
}
```

---



