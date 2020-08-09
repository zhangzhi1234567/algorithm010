# leetcode_746.使用最小花费爬楼梯

数组的每个索引作为一个阶梯，第 i个阶梯对应着一个非负数的体力花费值 cost[i](索引从0开始)。


每当你爬上一个阶梯你都要花费对应的体力花费值，然后你可以选择继续爬一个阶梯或者爬两个阶梯。


您需要找到达到楼层顶部的最低花费。在开始时，你可以选择从索引为 0 或 1 的元素作为初始阶梯。
链接：[https://leetcode-cn.com/problems/min-cost-climbing-stairs](https://leetcode-cn.com/problems/min-cost-climbing-stairs)


```
输入: cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
输出: 6
解释: 最低花费方式是从cost[0]开始，逐个经过那些1，跳过cost[3]，一共花费6
```




### 动态规划
/*
跳出最后，肯定是从最后一层跳过去，或者从倒数第二层跳过去；
即化作求第i个阶梯花费的体力；
dp[i]表示跳过i花费的较小的步数: dp[i] = min(dp[i-2], dp[i-1]) + cost[i]


最后一步踏上第0级台阶，最小花费dp[0] = cost[0]。
最后一步踏上第1级台阶有两个选择：
可以分别踏上第0级与第1级台阶，花费cost[0] + cost[1]；
也可以从地面开始迈两步直接踏上第1级台阶，花费cost[1]。
最小值dp[1] = min(cost[0] + cost[1], cost[1]) = cost[1]
*/


```cpp
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        int len = cost.size();
        vector<int> dp(len + 1, 0);
        dp[0] = cost[0];
        dp[1] = cost[1];
        for (int i = 2; i < len; i++) {
            dp[i] = min(dp[i-1], dp[i-2]) + cost[i];
        }
        return min(dp[len - 1], dp[len - 2]);
    }
};
```
