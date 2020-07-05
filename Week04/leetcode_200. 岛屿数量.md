# leetcode_200. 岛屿数量

给你一个由  '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。
岛屿总是被水包围，并且每座岛屿只能由水平方向或竖直方向上相邻的陆地连接形成。
此外，你可以假设该网格的四条边均被水包围。
```
输入:
11110
11010
11000
00000
输出: 1
```
### c plus

---

- DFS
```
class Solution {
public:
    int n;
    int m;
    int numIslands(vector<vector<char>>& grid) {
        if (grid.empty())   return 0;
        n = grid.size();
        m = grid[0].size();
        int count = 0;
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) { //遍历二维数组
                if (grid[i][j] == '1') {  //发现岛屿，置为0，数量加1， 并查找每一个‘1’水平和竖直方向,
                    dfsMarkZero(i, j, grid);
                    count++;
                }
            }
        }
        return count;
    }
    void dfsMarkZero(int i, int j, vector<vector<char>>& grid) {
        if (i < 0 || j < 0 || i >= n || j >= m || grid[i][j] == '0') return;
        grid[i][j] = '0';
        dfsMarkZero(i - 1, j, grid);
        dfsMarkZero(i + 1, j, grid);
        dfsMarkZero(i, j - 1, grid);
        dfsMarkZero(i, j + 1, grid);
    }
};
```

---

%E7%BB%99%E4%BD%A0%E4%B8%80%E4%B8%AA%E7%94%B1%C2%A0'1'%EF%BC%88%E9%99%86%E5%9C%B0%EF%BC%89%E5%92%8C%20'0'%EF%BC%88%E6%B0%B4%EF%BC%89%E7%BB%84%E6%88%90%E7%9A%84%E7%9A%84%E4%BA%8C%E7%BB%B4%E7%BD%91%E6%A0%BC%EF%BC%8C%E8%AF%B7%E4%BD%A0%E8%AE%A1%E7%AE%97%E7%BD%91%E6%A0%BC%E4%B8%AD%E5%B2%9B%E5%B1%BF%E7%9A%84%E6%95%B0%E9%87%8F%E3%80%82%0A%0A%E5%B2%9B%E5%B1%BF%E6%80%BB%E6%98%AF%E8%A2%AB%E6%B0%B4%E5%8C%85%E5%9B%B4%EF%BC%8C%E5%B9%B6%E4%B8%94%E6%AF%8F%E5%BA%A7%E5%B2%9B%E5%B1%BF%E5%8F%AA%E8%83%BD%E7%94%B1%E6%B0%B4%E5%B9%B3%E6%96%B9%E5%90%91%E6%88%96%E7%AB%96%E7%9B%B4%E6%96%B9%E5%90%91%E4%B8%8A%E7%9B%B8%E9%82%BB%E7%9A%84%E9%99%86%E5%9C%B0%E8%BF%9E%E6%8E%A5%E5%BD%A2%E6%88%90%E3%80%82%0A%0A%E6%AD%A4%E5%A4%96%EF%BC%8C%E4%BD%A0%E5%8F%AF%E4%BB%A5%E5%81%87%E8%AE%BE%E8%AF%A5%E7%BD%91%E6%A0%BC%E7%9A%84%E5%9B%9B%E6%9D%A1%E8%BE%B9%E5%9D%87%E8%A2%AB%E6%B0%B4%E5%8C%85%E5%9B%B4%E3%80%82%0A%60%60%60%0A%E8%BE%93%E5%85%A5%3A%0A11110%0A11010%0A11000%0A00000%0A%E8%BE%93%E5%87%BA%3A%201%0A%60%60%60%0A%0A%23%23%23%20c%20plus%0A%0A*%20*%20*%0A*%20DFS%0A%60%60%60c%0Aclass%20Solution%20%7B%0Apublic%3A%0A%20%20%20%20int%20n%3B%0A%20%20%20%20int%20m%3B%0A%20%20%20%20int%20numIslands(vector%3Cvector%3Cchar%3E%3E%26%20grid)%20%7B%0A%20%20%20%20%20%20%20%20if%20(grid.empty())%20%20%20return%200%3B%0A%20%20%20%20%20%20%20%20n%20%3D%20grid.size()%3B%0A%20%20%20%20%20%20%20%20m%20%3D%20grid%5B0%5D.size()%3B%0A%20%20%20%20%20%20%20%20int%20count%20%3D%200%3B%0A%20%20%20%20%20%20%20%20for%20(int%20i%20%3D%200%3B%20i%20%3C%20n%3B%20%2B%2Bi)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20for%20(int%20j%20%3D%200%3B%20j%20%3C%20m%3B%20%2B%2Bj)%20%7B%20%2F%2F%E9%81%8D%E5%8E%86%E4%BA%8C%E7%BB%B4%E6%95%B0%E7%BB%84%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20if%20(grid%5Bi%5D%5Bj%5D%20%3D%3D%20'1')%20%7B%20%20%2F%2F%E5%8F%91%E7%8E%B0%E5%B2%9B%E5%B1%BF%EF%BC%8C%E7%BD%AE%E4%B8%BA0%EF%BC%8C%E6%95%B0%E9%87%8F%E5%8A%A01%EF%BC%8C%20%E5%B9%B6%E6%9F%A5%E6%89%BE%E6%AF%8F%E4%B8%80%E4%B8%AA%E2%80%981%E2%80%99%E6%B0%B4%E5%B9%B3%E5%92%8C%E7%AB%96%E7%9B%B4%E6%96%B9%E5%90%91%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20dfsMarkZero(i%2C%20j%2C%20grid)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20count%2B%2B%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20return%20count%3B%0A%20%20%20%20%7D%0A%0A%20%20%20%20void%20dfsMarkZero(int%20i%2C%20int%20j%2C%20vector%3Cvector%3Cchar%3E%3E%26%20grid)%20%7B%0A%20%20%20%20%20%20%20%20if%20(i%20%3C%200%20%7C%7C%20j%20%3C%200%20%7C%7C%20i%20%3E%3D%20n%20%7C%7C%20j%20%3E%3D%20m%20%7C%7C%20grid%5Bi%5D%5Bj%5D%20%3D%3D%20'0')%20return%3B%0A%20%20%20%20%20%20%20%20grid%5Bi%5D%5Bj%5D%20%3D%20'0'%3B%0A%20%20%20%20%20%20%20%20dfsMarkZero(i%20-%201%2C%20j%2C%20grid)%3B%0A%20%20%20%20%20%20%20%20dfsMarkZero(i%20%2B%201%2C%20j%2C%20grid)%3B%0A%20%20%20%20%20%20%20%20dfsMarkZero(i%2C%20j%20-%201%2C%20grid)%3B%0A%20%20%20%20%20%20%20%20dfsMarkZero(i%2C%20j%20%2B%201%2C%20grid)%3B%0A%20%20%20%20%7D%0A%7D%3B%0A%60%60%60%0A%0A*%20*%20*%0A
