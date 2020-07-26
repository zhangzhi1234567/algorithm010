# leetcode_212.单词搜索

给定一个二维网格 board 和一个字典中的单词列表 words，找出所有同时在二维网格和字典中出现的单词。


单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母在一个单词中不允许被重复使用。
```
输入: 
words = ["oath","pea","eat","rain"] and board =
[
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]

输出: ["eat","oath"]
```
### Trie


```cpp
class Trie {
    struct TrieNode {
    bool end;
    string str;
    unordered_map<char, TrieNode *> child;
    TrieNode(): end(false), str("") {};
};
public:
    Trie() {
        root = new TrieNode();
    }
    void insert(string word) {
        TrieNode *cur = root;
        for (int i = 0; i < word.size(); i++) {
            if (cur->child.count(word[i]) == 0) {
                cur->child[word[i]] = new TrieNode();
            }
            cur = cur->child[word[i]];
        }
        cur->str = word;             //下一个节点存单词， 当前节点不存。
        cur->end = true;
    }

    void search(vector<string>& res, vector<vector<char>>& board) {
        for (int i = 0; i < board.size(); i++) {
            for (int j = 0; j < board[i].size(); j++) {
                help(res, board, root, i, j);
            }
        }
    }
    void help(vector<string>& res, vector<vector<char>>& board, TrieNode *p, int x, int y) {
        if (p->end) {      //因为trie树把单词存入下一个节点，所以这里进来就判断是不是单词结尾，走到该处，说明有一个完整的单词
            res.push_back(p->str);
            p->end = false; //防止重复添加
            return;
        }
        if (x < 0 || x == board.size() || y < 0 || y == board[x].size()) return; //判断边界
        if (p->child.find(board[x][y]) == p->child.end()) return; //当前节点的map中找不到board中四通图的字符则返回
        //下面是找到了字符
        p = p->child[board[x][y]]; //找下一个节点，下一个节点end为true的话，说明找到了完整的单词
        char cur = board[x][y];
        board[x][y] = '#';
        help(res, board, p, x + 1, y); //不能先算减一
        help(res, board, p, x - 1, y);
        help(res, board, p, x, y + 1); //同上
        help(res, board, p, x, y - 1);
        board[x][y] = cur;
    }
private:
    TrieNode *root;

};

class Solution {
public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        Trie trie;
        for (string &w : words) {
            trie.insert(w);
        }
        vector<string> res;
        trie.search(res, board);
        return res;
    }
};


```
