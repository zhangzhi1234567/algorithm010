# leetcode_433.最小基因变化

一条基因序列由一个带有8个字符的字符串表示，其中每个字符都属于 "A", "C", "G", "T"中的任意一个。
假设我们要调查一个基因序列的变化。一次基因变化意味着这个基因序列中的一个字符发生了变化。
例如，基因序列由"AACCGGTT" 变化至 "AACCGGTA" 即发生了一次基因变化。
与此同时，每一次基因变化的结果，都需要是一个合法的基因串，即该结果属于一个基因库。
现在给定3个参数 — start, end, bank，分别代表起始基因序列，目标基因序列及基因库，请找出能够使起始基因序列变化为目标基因序列所需的最少变化次数。如果无法实现目标变化，请返回 -1。
注意:
起始基因序列默认是合法的，但是它并不一定会出现在基因库中。
所有的目标基因序列必须是合法的。
假定起始基因序列与目标基因序列是不一样的。
链接：[https://leetcode-cn.com/problems/minimum-genetic-mutation](https://leetcode-cn.com/problems/minimum-genetic-mutation)
```
start: "AAAAACCC"
end:   "AACCCCCC"
bank: ["AAAACCCC", "AAACCCCC", "AACCCCCC"]

返回值: 3
```
### BFS

- **和单词接龙一样的思路**
```cpp
class Solution {
public:
    int minMutation(string start, string end, vector<string>& bank) {
        unordered_set<string> bankSet(bank.begin(), bank.end());
        unordered_set<string> visited;
        if (bankSet.find(end) == bankSet.end()) return -1;
        queue<string> queueTodo;
        queueTodo.push(start);
        int count = 0;
        while (!queueTodo.empty()) {
            int queueLen = queueTodo.size();
            for (int i = 0; i < queueLen; i++) {
                string cur = queueTodo.front(); queueTodo.pop();
                for (int j = 0; j < cur.size(); j++) {
                    char old = cur[j];
                    for (char c: "ACGT") {
                        cur[j] = c;
                        if (cur[j] == old) continue;
                        if (cur == end) return count + 1;
                        if (bankSet.find(cur) != bankSet.end() && visited.find(cur) == visited.end()) {
                            queueTodo.push(cur);
                            visited.insert(cur);
                        }
                    }
                    cur[j] = old;
                }
            }
            count++;
        }
        return -1;
    }
};

```
### 双向BFS
复习时补上


























