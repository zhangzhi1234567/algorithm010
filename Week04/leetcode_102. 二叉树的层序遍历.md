# leetcode_102. 二叉树的层序遍历

给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。
```
示例：
二叉树：[3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：
[
  [3],
  [9,20],
  [15,7]
]
```
### c plus

---

- BFS
[题解](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/solution/tao-mo-ban-bfs-he-dfs-du-ke-yi-jie-jue-by-fuxuemin/)

```
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {//广度优先
        if(!root) return {};
        vector<vector<int>> res;
        queue<TreeNode *> q;   //辅助队列
        q.push(root);         //先处理根节点
        while(!q.empty()) {
            vector<int> level;
            int size = q.size();
            for(int i = 0; i < size; ++i) {
                //当前节点出队列,并处理
                TreeNode *cur = q.front(); q.pop();
                level.push_back(cur->val);
                //当前节点的相关节点入队列
                if (cur->left) q.push(cur->left);
                if (cur->right) q.push(cur->right);
            }
            //将当前层的结果添加到最终结果
            res.push_back(level);
        }
        return res;
    }
};
```

- DFS
> DFS 做本题的主要问题是： DFS 不是按照层次遍历的。为了让递归的过程中同一层的节点放到同一个列表中，在递归时要记录每个节点的深度 level。递归到新节点要把该节点放入 level 对应列表的末尾。
> 当遍历到一个新的深度 level，而最终结果 res 中还没有创建 level 对应的列表时，应该在 res 中新建一个列表用来保存该 level 的所有节点。

```
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {//深度优先
        vector<vector<int>> res;
        dfs(res, root, 0);
        return res;
    }
    void dfs(vector<vector<int>>& res, TreeNode *root, int level) {
        if (!root) return ;
        //process cur
        if (level >= res.size()) //要通过索引访问，要提前push_back
            res.push_back(vector<int>());
        res[level].push_back(root->val);
        //
        dfs(res, root->left, level + 1);
        dfs(res, root->right, level + 1);
    }
};
```

---

### golang

---

- BFS
```
func levelOrder(root *TreeNode) [][]int {
    if root == nil {
        return [][]int{}
    }
    res := make([][]int, 0)
    queue := make([]*TreeNode, 0)
    queue = append(queue, root)
    for len(queue) > 0 {
        level := []int{}
        l := len(queue)
        //处理当前层节点
        for i := 0; i < l; i++ {
            cur := queue[i]
            level = append(level, cur.Val)
            if cur.Left != nil {
                queue = append(queue, cur.Left)//把当前层节点的相连节点入队列
            }
            if cur.Right != nil {
                queue = append(queue, cur.Right)
            }   
        }
        //把当前层添加到结果中去
        res = append(res, level)
        queue = queue[l:]            //切片模拟队列，用偏移的方式模拟出队列
    }
    return res
}
```

---

%E7%BB%99%E4%BD%A0%E4%B8%80%E4%B8%AA%E4%BA%8C%E5%8F%89%E6%A0%91%EF%BC%8C%E8%AF%B7%E4%BD%A0%E8%BF%94%E5%9B%9E%E5%85%B6%E6%8C%89%20%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86%20%E5%BE%97%E5%88%B0%E7%9A%84%E8%8A%82%E7%82%B9%E5%80%BC%E3%80%82%20%EF%BC%88%E5%8D%B3%E9%80%90%E5%B1%82%E5%9C%B0%EF%BC%8C%E4%BB%8E%E5%B7%A6%E5%88%B0%E5%8F%B3%E8%AE%BF%E9%97%AE%E6%89%80%E6%9C%89%E8%8A%82%E7%82%B9%EF%BC%89%E3%80%82%0A%60%60%60%0A%E7%A4%BA%E4%BE%8B%EF%BC%9A%0A%E4%BA%8C%E5%8F%89%E6%A0%91%EF%BC%9A%5B3%2C9%2C20%2Cnull%2Cnull%2C15%2C7%5D%2C%0A%0A%20%20%20%203%0A%20%20%20%2F%20%5C%0A%20%209%20%2020%0A%20%20%20%20%2F%20%20%5C%0A%20%20%2015%20%20%207%0A%E8%BF%94%E5%9B%9E%E5%85%B6%E5%B1%82%E6%AC%A1%E9%81%8D%E5%8E%86%E7%BB%93%E6%9E%9C%EF%BC%9A%0A%0A%5B%0A%20%20%5B3%5D%2C%0A%20%20%5B9%2C20%5D%2C%0A%20%20%5B15%2C7%5D%0A%5D%0A%60%60%60%0A%0A%0A%23%23%23%20c%20plus%0A*%20*%20*%0A*%20BFS%0A%20%20%20%20%0A%20%20%20%20%5B%E9%A2%98%E8%A7%A3%5D(https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fbinary-tree-level-order-traversal%2Fsolution%2Ftao-mo-ban-bfs-he-dfs-du-ke-yi-jie-jue-by-fuxuemin%2F)%0A%60%60%60c%0Aclass%20Solution%20%7B%0Apublic%3A%0A%20%20%20%20vector%3Cvector%3Cint%3E%3E%20levelOrder(TreeNode*%20root)%20%7B%2F%2F%E5%B9%BF%E5%BA%A6%E4%BC%98%E5%85%88%0A%20%20%20%20%20%20%20%20if(!root)%20return%20%7B%7D%3B%0A%20%20%20%20%20%20%20%20vector%3Cvector%3Cint%3E%3E%20res%3B%0A%20%20%20%20%20%20%20%20queue%3CTreeNode%20*%3E%20q%3B%20%20%20%2F%2F%E8%BE%85%E5%8A%A9%E9%98%9F%E5%88%97%0A%20%20%20%20%20%20%20%20q.push(root)%3B%20%20%20%20%20%20%20%20%20%2F%2F%E5%85%88%E5%A4%84%E7%90%86%E6%A0%B9%E8%8A%82%E7%82%B9%0A%20%20%20%20%20%20%20%20while(!q.empty())%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20vector%3Cint%3E%20level%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20int%20size%20%3D%20q.size()%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20for(int%20i%20%3D%200%3B%20i%20%3C%20size%3B%20%2B%2Bi)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%2F%2F%E5%BD%93%E5%89%8D%E8%8A%82%E7%82%B9%E5%87%BA%E9%98%9F%E5%88%97%2C%E5%B9%B6%E5%A4%84%E7%90%86%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20TreeNode%20*cur%20%3D%20q.front()%3B%20q.pop()%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20level.push_back(cur-%3Eval)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%2F%2F%E5%BD%93%E5%89%8D%E8%8A%82%E7%82%B9%E7%9A%84%E7%9B%B8%E5%85%B3%E8%8A%82%E7%82%B9%E5%85%A5%E9%98%9F%E5%88%97%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20if%20(cur-%3Eleft)%20q.push(cur-%3Eleft)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20if%20(cur-%3Eright)%20q.push(cur-%3Eright)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%2F%2F%E5%B0%86%E5%BD%93%E5%89%8D%E5%B1%82%E7%9A%84%E7%BB%93%E6%9E%9C%E6%B7%BB%E5%8A%A0%E5%88%B0%E6%9C%80%E7%BB%88%E7%BB%93%E6%9E%9C%0A%20%20%20%20%20%20%20%20%20%20%20%20res.push_back(level)%3B%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20return%20res%3B%0A%20%20%20%20%7D%0A%7D%3B%0A%60%60%60%0A%0A*%20DFS%0A%3EDFS%20%E5%81%9A%E6%9C%AC%E9%A2%98%E7%9A%84%E4%B8%BB%E8%A6%81%E9%97%AE%E9%A2%98%E6%98%AF%EF%BC%9A%20DFS%20%E4%B8%8D%E6%98%AF%E6%8C%89%E7%85%A7%E5%B1%82%E6%AC%A1%E9%81%8D%E5%8E%86%E7%9A%84%E3%80%82%E4%B8%BA%E4%BA%86%E8%AE%A9%E9%80%92%E5%BD%92%E7%9A%84%E8%BF%87%E7%A8%8B%E4%B8%AD%E5%90%8C%E4%B8%80%E5%B1%82%E7%9A%84%E8%8A%82%E7%82%B9%E6%94%BE%E5%88%B0%E5%90%8C%E4%B8%80%E4%B8%AA%E5%88%97%E8%A1%A8%E4%B8%AD%EF%BC%8C%E5%9C%A8%E9%80%92%E5%BD%92%E6%97%B6%E8%A6%81%E8%AE%B0%E5%BD%95%E6%AF%8F%E4%B8%AA%E8%8A%82%E7%82%B9%E7%9A%84%E6%B7%B1%E5%BA%A6%20level%E3%80%82%E9%80%92%E5%BD%92%E5%88%B0%E6%96%B0%E8%8A%82%E7%82%B9%E8%A6%81%E6%8A%8A%E8%AF%A5%E8%8A%82%E7%82%B9%E6%94%BE%E5%85%A5%20level%20%E5%AF%B9%E5%BA%94%E5%88%97%E8%A1%A8%E7%9A%84%E6%9C%AB%E5%B0%BE%E3%80%82%0A%3E%E5%BD%93%E9%81%8D%E5%8E%86%E5%88%B0%E4%B8%80%E4%B8%AA%E6%96%B0%E7%9A%84%E6%B7%B1%E5%BA%A6%20level%EF%BC%8C%E8%80%8C%E6%9C%80%E7%BB%88%E7%BB%93%E6%9E%9C%20res%20%E4%B8%AD%E8%BF%98%E6%B2%A1%E6%9C%89%E5%88%9B%E5%BB%BA%20level%20%E5%AF%B9%E5%BA%94%E7%9A%84%E5%88%97%E8%A1%A8%E6%97%B6%EF%BC%8C%E5%BA%94%E8%AF%A5%E5%9C%A8%20res%20%E4%B8%AD%E6%96%B0%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%88%97%E8%A1%A8%E7%94%A8%E6%9D%A5%E4%BF%9D%E5%AD%98%E8%AF%A5%20level%20%E7%9A%84%E6%89%80%E6%9C%89%E8%8A%82%E7%82%B9%E3%80%82%0A%60%60%60C%0Aclass%20Solution%20%7B%0Apublic%3A%0A%20%20%20%20vector%3Cvector%3Cint%3E%3E%20levelOrder(TreeNode*%20root)%20%7B%2F%2F%E6%B7%B1%E5%BA%A6%E4%BC%98%E5%85%88%0A%20%20%20%20%20%20%20%20vector%3Cvector%3Cint%3E%3E%20res%3B%0A%20%20%20%20%20%20%20%20dfs(res%2C%20root%2C%200)%3B%0A%20%20%20%20%20%20%20%20return%20res%3B%0A%20%20%20%20%7D%0A%0A%20%20%20%20void%20dfs(vector%3Cvector%3Cint%3E%3E%26%20res%2C%20TreeNode%20*root%2C%20int%20level)%20%7B%0A%20%20%20%20%20%20%20%20if%20(!root)%20return%20%3B%0A%20%20%20%20%20%20%20%20%2F%2Fprocess%20cur%0A%20%20%20%20%20%20%20%20if%20(level%20%3E%3D%20res.size())%20%2F%2F%E8%A6%81%E9%80%9A%E8%BF%87%E7%B4%A2%E5%BC%95%E8%AE%BF%E9%97%AE%EF%BC%8C%E8%A6%81%E6%8F%90%E5%89%8Dpush_back%0A%20%20%20%20%20%20%20%20%20%20%20%20res.push_back(vector%3Cint%3E())%3B%0A%20%20%20%20%20%20%20%20res%5Blevel%5D.push_back(root-%3Eval)%3B%0A%20%20%20%20%20%20%20%20%2F%2F%0A%20%20%20%20%20%20%20%20dfs(res%2C%20root-%3Eleft%2C%20level%20%2B%201)%3B%0A%20%20%20%20%20%20%20%20dfs(res%2C%20root-%3Eright%2C%20level%20%2B%201)%3B%0A%20%20%20%20%7D%0A%7D%3B%0A%0A%60%60%60%0A%0A%0A%0A*%20*%20*%0A%0A%23%23%23%20golang%0A%0A*%20*%20*%0A*%20BFS%0A%60%60%60go%0Afunc%20levelOrder(root%20*TreeNode)%20%5B%5D%5B%5Dint%20%7B%0A%20%20%20%20if%20root%20%3D%3D%20nil%20%7B%0A%20%20%20%20%20%20%20%20return%20%5B%5D%5B%5Dint%7B%7D%0A%20%20%20%20%7D%0A%20%20%20%20res%20%3A%3D%20make(%5B%5D%5B%5Dint%2C%200)%0A%20%20%20%20queue%20%3A%3D%20make(%5B%5D*TreeNode%2C%200)%0A%20%20%20%20queue%20%3D%20append(queue%2C%20root)%0A%20%20%20%20for%20len(queue)%20%3E%200%20%7B%0A%20%20%20%20%20%20%20%20level%20%3A%3D%20%5B%5Dint%7B%7D%0A%20%20%20%20%20%20%20%20l%20%3A%3D%20len(queue)%0A%20%20%20%20%20%20%20%20%2F%2F%E5%A4%84%E7%90%86%E5%BD%93%E5%89%8D%E5%B1%82%E8%8A%82%E7%82%B9%0A%20%20%20%20%20%20%20%20for%20i%20%3A%3D%200%3B%20i%20%3C%20l%3B%20i%2B%2B%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20cur%20%3A%3D%20queue%5Bi%5D%0A%20%20%20%20%20%20%20%20%20%20%20%20level%20%3D%20append(level%2C%20cur.Val)%0A%20%20%20%20%20%20%20%20%20%20%20%20if%20cur.Left%20!%3D%20nil%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20queue%20%3D%20append(queue%2C%20cur.Left)%2F%2F%E6%8A%8A%E5%BD%93%E5%89%8D%E5%B1%82%E8%8A%82%E7%82%B9%E7%9A%84%E7%9B%B8%E8%BF%9E%E8%8A%82%E7%82%B9%E5%85%A5%E9%98%9F%E5%88%97%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20if%20cur.Right%20!%3D%20nil%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20queue%20%3D%20append(queue%2C%20cur.Right)%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%20%20%20%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%2F%2F%E6%8A%8A%E5%BD%93%E5%89%8D%E5%B1%82%E6%B7%BB%E5%8A%A0%E5%88%B0%E7%BB%93%E6%9E%9C%E4%B8%AD%E5%8E%BB%0A%20%20%20%20%20%20%20%20res%20%3D%20append(res%2C%20level)%0A%20%20%20%20%20%20%20%20queue%20%3D%20queue%5Bl%3A%5D%20%20%20%20%20%20%20%20%20%20%20%20%2F%2F%E5%88%87%E7%89%87%E6%A8%A1%E6%8B%9F%E9%98%9F%E5%88%97%EF%BC%8C%E7%94%A8%E5%81%8F%E7%A7%BB%E7%9A%84%E6%96%B9%E5%BC%8F%E6%A8%A1%E6%8B%9F%E5%87%BA%E9%98%9F%E5%88%97%0A%20%20%20%20%7D%0A%20%20%20%20return%20res%0A%7D%0A%60%60%60%0A%0A%0A%0A*%20*%20*%0A
