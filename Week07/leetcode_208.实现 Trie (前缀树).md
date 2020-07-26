# leetcode_208.实现 Trie (前缀树)

字典树
实现一个 Trie (前缀树)，包含 `insert`, `search`, 和 `startsWith` 这三个操作。
```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // 返回 true
trie.search("app");     // 返回 false
trie.startsWith("app"); // 返回 true
trie.insert("app");   
trie.search("app");     // 返回 true
```


a
|
[b c d]
|   |----|
[e f g]    [h i k]
插入即按单词的字符循环插入，如果当前节点已经有了当前字符，就不用新开辟一个节点。
查找即按单词的字符循环查找节点对应的map，如果没有，即返回失败。
**map里存的是每个字母后面连接的其他所有字母**
```cpp
class Trie {
    struct TrieNode {
        map<char, TrieNode *> child_table;//map索引为当前字母；值指向下一级node，下一级node也存放一个map表。
        int end;						  //也就是说每一个字母的下一级都会维护一个map表。
        TrieNode(): end(0) {};
    };
public:
    /** Initialize your data structure here. */
    Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        TrieNode *cur = root;
        for (int i = 0; i < word.size(); i++) {
            if (cur->child_table.count(word[i]) == 0) {
                cur->child_table[word[i]] = new TrieNode();
            }
            cur = cur->child_table[word[i]];
        }
        cur->end = 1;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        return find(word, 1);
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        return find(prefix, 0);
    }
private:
    bool find(string word, int extra_flag) { //查找即按层查找单词对应的字符。没有就返回false,有，且word查找到最后则看end标志位。
        TrieNode *cur = root;
        for (int i = 0; i < word.size(); i++) {
            if (cur->child_table.count(word[i]) == 0) {
                return false;
            }
            cur = cur->child_table[word[i]];
        }
        if (extra_flag) {
            return (cur->end) ? true : false;
        }else {
            return true;
        }
    }
private:
    TrieNode *root;
};

```


```cpp
class Trie {
	struct TrieNode {
    	unorder_map<char, TrieNode*> child;
        int end;
        TrieNode():end(0){};
    };



};



```


