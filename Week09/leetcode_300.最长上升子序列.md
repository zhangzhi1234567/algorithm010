# leetcode_300.最长上升子序列

给定一个无序的整数数组，找到其中最长上升子序列的长度。
```
输入: [10,9,2,5,3,7,101,18]
输出: 4 
解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。
```


- 动态规划



时间复杂度为o(n^2)
**再次注意 状态数组和前面的DP[I]比较到最大最小值的写法**
```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int len = nums.size();
        if (len < 2) return len;
        vector<int> dp(len, 1);
        int res = 0;
        for (int i = 1; i < len; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = max(dp[i], dp[j] + 1);
                }
            }
            if (dp[i] >= res) res = dp[i];
        }
        return res;
    }
};
```


