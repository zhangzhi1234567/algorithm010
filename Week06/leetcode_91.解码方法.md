# leetcode_91.解码方法

动态规划
一条包含字母 `A-Z` 的消息通过以下方式进行了编码：
'A' -> 1
'B' -> 2
...
'Z' -> 26
给定一个只包含数字的**非空**字符串，请计算解码方法的总数。
```
输入: "12"
输出: 2
解释: 它可以解码为 "AB"（1 2）或者 "L"（12）。

输入: "226"
输出: 3
解释: 它可以解码为 "BZ" (2 26), "VF" (22 6), 或者 "BBF" (2 2 6) 。
```


### 动态规划

---

/*
dp[i] 表示第i个位置有多少种编码
dp[i] = 可以由dp[i-1]然后加上第i个位置的编码， 也可以由dp[i-2],然后加上第i-1到i个位置组成的编码。类似于爬楼梯，最后一步从最后一阶上，和最后一步从最后两阶上。
前提：
if i == 0 
    if i-1 == '1' || '2'         ---2 1 0
        dp[i] = dp[i-2]
    else 
  return 0
if i - 1 == '1' 则不用考虑i 因为10~19都可以
     dp[i] = dp[i-1] + dp[i-2]
if i -1 == '2' 
    if "1"<= i <= "6" dp[i] = dp[i-1] + dp[i-2]
else 
dp[i] = dp[i-1];
*/
```cpp
class Solution {
public:
    int numDecodings(string s) {
        if (s[0] == '0') return 0;
        int len = s.size();
        vector<int> dp(len + 1, 0);
        dp[0] = 1; dp[1] = 1;
        for (int i = 1; i < len; i++) {
            if (s[i] == '0') {
                if (s[i-1] == '1' || s[i-1] == '2')
                    dp[i+1] = dp[i-1];
                else
                    return 0;
            }else {
                if ((s[i-1] == '1') || (s[i-1] == '2' && s[i] <= '6')){
                    dp[i+1] = dp[i] + dp[i-1];
                }else {
                    dp[i+1] = dp[i];
                }
            } 
        }
        return dp[len];
    }
};

```
