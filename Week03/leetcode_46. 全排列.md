给定一个 没有重复 数字的序列，返回其所有可能的全排列。
```
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```
### c plus

* * *
* 回溯
  需要重点理解回溯算法

  [题解](https://leetcode-cn.com/problems/permutations/solution/hui-su-suan-fa-python-dai-ma-java-dai-ma-by-liweiw/)
```c
class Solution {
public:
    vector<vector<int>> res;
    vector<vector<int>> permute(vector<int>& nums) {
       if (nums.size() <= 1) {
            res.push_back(nums);
            return res;
       }
     
       vector<int> cur;
       vector<bool> used(nums.size(), false);
       helper(cur, used, nums);
       return res;
    }
    void  helper(vector<int>& cur, vector<bool>& used, vector<int>& nums) {
        if (cur.size() == nums.size()) {
            return res.push_back(cur);
        }
        for (int i = 0; i < nums.size(); ++i) {
            if (!used[i]){
                used[i] = true;
                cur.push_back(nums[i]);
                helper(cur, used, nums);
                used[i] = false;
                cur.pop_back();
            }
        }
    } 
};

```

* * *
