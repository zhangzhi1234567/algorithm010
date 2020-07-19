# leetcode_198. 打家劫舍

动态规划、升维思想
你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。


给定一个代表每个房屋存放金额的非负整数数组，计算你 不触动警报装置的情况下 ，一夜之内能够偷窃到的最高金额。
链接：[https://leetcode-cn.com/problems/house-robber](https://leetcode-cn.com/problems/house-robber)


```
输入：[1,2,3,1]
输出：4
解释：偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
     偷窃到的最高金额 = 1 + 3 = 4 。
```
### 动态规划

---

- 二维DP

/*
subproblem: 
sub[i] 表示偷第i个房间时的最高金额数
第i个房间有可能偷 有可能不偷， 需要升维表示偷或不偷的状态
sub[i][0] 表示第i个房间不偷 sub[i][0] = max(sub[i-1][1], sub[i-1][0])  当前不偷，前一个就可以偷或者不偷，则结果等于前一个偷或者不偷的子结构的最大值。          
sub[i][1] 表示第i个房间偷   sub[i][1] = sub[i-1][0] + nums[i]      当前房间偷，前一个肯定不偷，则结果就是前一个不偷的子结构加上自己 


状态数组： dp[i][0] dp[i][1]
DP方程：
sub[i][0] = max(sub[i-1][1], sub[i-1][0])
sub[i][1] = sub[i-1][0] + nums[i]
*/
```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int len = nums.size();
        if (len == 0) {
            return 0;
        }
        vector<vector<int>> dp(len, vector<int>(2,0));
        dp[0][0] = 0;
        dp[0][1] = nums[0];
        for (int i = 1; i < len; i++) {
            dp[i][0] = max(dp[i-1][1], dp[i-1][0]);
            dp[i][1] = dp[i-1][0] + nums[i];
        }
        return dp[len-1][0] > dp[len-1][1] ? dp[len-1][0] : dp[len-1][1];
    }
};


```


- 一维DP

/*
一维的方式：
子问题：定义sub[i]表示第i房间的最高金额数 则sub[i]就等于前一个偷的房间的最高金额，或者前两个偷的房间加上本房间的
状态数组：dp[i]
DP方程：dp[i] = max(dp[i-1], dp[i-2]+nums[i])
*/
```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int len = nums.size();
        if (len == 0) return 0;
        if (len == 1) return nums[0];
        vector<int> dp(len, 0);
        dp[0] = nums[0];
        dp[1] = max(nums[0], nums[1]);
        for (int i = 2; i < len; i++) {
            dp[i] = max(dp[i-1], dp[i-2] + nums[i]);
        }
        return dp[len-1];
    }
};
--将空间复杂度优化成O(1)
--还是参照着 dp[i] = max(dp[i - 1], dp[i - 2] + nums[i]) 这个方程来写，
--用 a 表示 i - 2，b 表示 i - 1，因此上面的方程变成了dp[i] = max(b, a + nums[i])，
--相当于从后往前推 i-2 = a; i-1 = b; i=c; 最后一个是a，则下一轮循环时就是将a往前移动位置即 a = b;同理，b = c;
class Solution {
public:
    int rob(vector<int>& nums) {
        int len = nums.size();
        if (len == 0) return 0;
        if (len == 1) return nums[0];
        int a = 0;//dp[i-2]
        int b = 0;//dp[i-1]
        for (int i = 0; i < len; i++) {
            int c = max(b, a + nums[i]);
            a = b;
            b = c;
        }
        return b;
    }
};


```
