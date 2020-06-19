给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。(出现的相同字母次数相同)
```
输入: s = "anagram", t = "nagaram"
输出: true
```

### c plus 
***

* **排序法**
```c
class Solution {
public:
       bool isAnagram(string s, string t) {
            if (s.size() != t.size()) return false;
            sort(s.begin(), s.end());
            sort(t.begin(), t.end());
            return s == t;
       }
 };

```

* 哈希

```c
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.size() != t.size()) return false;

        char array[26];
        memset(array, 0, 26);

        for (int i = 0; i < s.size(); i++) {
            array[s[i] % 26]++;
        }
        for (int i = 0; i < t.size(); i++) {
            array[t[i] % 26]--;
        }
        for (int i = 0; i < 26; i++) {
            if (array[i] != 0)  return false; 
        }
        return true;
    }
};

//上面写的有点啰嗦，改一下：
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.size() != t.size()) return false;
        int n = s.size();
        char array[26];
        memset(array, 0, 26);
        for (int i = 0; i < n; i++) {
            array[s[i] - 'a']++;
            array[t[i] - 'a']--;
        }
        for (int i = 0; i < 26; i++) {
            if (array[i] != 0)  return false; 
        }
        return true;
    }
};

```

***