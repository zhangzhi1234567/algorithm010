给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。
```
输入: ["eat", "tea", "tan", "ate", "nat", "bat"]
输出:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

### c plus
***

* 排序法
 ```c
//把每个单词排序，然后将排序后单词当成KEY放入哈希中， 哈希碰撞的即是结果
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> mp;
        for (string s : strs) {
            string tmp = s;
            sort(tmp.begin(), tmp.end());
            mp[tmp].push_back(s);
        }
        vector<vector<string>> ret;
        for (auto s : mp) {
            ret.push_back(s.second);
        }
        return ret;
    }
};
```


***