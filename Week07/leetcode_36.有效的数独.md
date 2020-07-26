# leetcode_36.有效的数独

判断一个 9x9 的数独是否有效。只需要根据以下规则，验证已经填入的数字是否有效即可。
数字 1-9 在每一行只能出现一次。
数字 1-9 在每一列只能出现一次。
数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。
链接：[https://leetcode-cn.com/problems/valid-sudoku](https://leetcode-cn.com/problems/valid-sudoku)
```
输入:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
输出: true
```
```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        vector<unordered_map<int, int>> rows(9), cols(9), blocks(9);
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] == '.') continue;
                int blo_index = (i/3)*3 + (j/3);
                int cur = board[i][j] - '0'; //字符转成Int
                if (rows[i].count(cur) || cols[j].count(cur) || blocks[blo_index].count(cur)) 
                    return false;
               
                rows[i][cur] = 1; //行记录一次 
                cols[j][cur] = 1; //列记录一次 
                blocks[blo_index][cur] = 1; //块记录一次   
            }
        }
        return true;
    }
};

//可简化成二维数组的形式，用二维数组记录状态。

```
