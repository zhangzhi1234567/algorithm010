给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。
```
    3
   / \
  9  20
    /  \
   15   7          返回它的最大深度 3 
```

### c plus
***

* **递归**
    
    [题解](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/solution/er-cha-shu-de-zui-da-shen-du-by-leetcode/)
```c
class Solution {
public:
    int maxDepth(TreeNode* root) {
        return helper(root);
    }
    int helper(TreeNode *node) {
        if (node == NULL)   return 0;
        int left = helper(node->left);
        int right = helper(node->right);
        return max(left, right) + 1;
    }
};
```
***

### Golang
***
```go

func maxDepth(root *TreeNode) int {
    if (root == nil){
        return 0
    }
    
    ld := maxDepth(root.Left)
    rd := maxDepth(root.Right)
    if ld > rd {
        return ld + 1
    }else{
        return rd + 1
    }
}
```

***