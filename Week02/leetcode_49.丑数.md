我们把只包含因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。
```
输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。
```

### c plus
***

* 动态规划

[题解](https://leetcode-cn.com/problems/chou-shu-lcof/solution/chou-shu-ii-qing-xi-de-tui-dao-si-lu-by-mrsate/)
```c
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> dp(n, 0);
        dp[0] = 1;
        int p2 = 0, p3 = 0, p5 = 0;//用三个快慢指针维护三个组数。
         
        for (int i = 1; i < n; i++) {
            dp[i] = min(min(dp[p2] * 2, dp[p3] * 3), dp[p5] * 5);
            if (dp[i] == dp[p2] * 2)
                p2++;
            if (dp[i] == dp[p3] * 3)
                p3++;
            if (dp[i] == dp[p5] * 5)
                p5++;   
        } 
        return dp[n - 1];
    }
};

```

***