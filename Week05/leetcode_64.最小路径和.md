# leetcode_64.最小路径和

动态规划 
给定一个包含非负整数的 _m_ x _n_ 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。
**说明：**每次只能向下或者向右移动一步。
```
输入:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 7
解释: 因为路径 1→3→1→1→1 的总和最小。
```


### 动态规划

---

/*
子问题： sub[i][j] = min(sub[i+1][j],sub[i][j+1]) + nums[i][j]
第一行：dp[i][j] = dp[i][j-1] + grid[i][j];
第一列：dp[i][j] = dp[i-1][j] + grid[i][j];
1 3 1
1 5 1
4 2 1
*/

1. 先把行和列初始化算好
```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int row = grid.size();
        int col = grid[0].size();
        vector<vector<int>> dp(row, vector<int>(col, 0));
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if(i ==0 && j == 0) dp[i][j] = grid[i][j];
                else if(i == 0 && j != 0) dp[i][j] = dp[i][j-1] + grid[i][j];
                else if(j == 0 && i != 0) dp[i][j] = dp[i-1][j] + grid[i][j];
                else dp[i][j] = min(dp[i-1][j],dp[i][j-1]) + grid[i][j];
            }
        } 
        return dp[row-1][col-1]; 
    }
};




```




























