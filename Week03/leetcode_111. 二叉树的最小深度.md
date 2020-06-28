
给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

说明: 叶子节点是指没有子节点的节点。
```
    3
   / \
  9  20
    /  \
   15   7
返回它的最小深度  2.
```

### c plus
***

* **递归**
  和最大深度不同的是要考虑左右子树一个为空一个不为空的情况，这种情况时，为空的子树的深度不可算在内
    
    [题解](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/solution/java-di-gui-he-fei-di-gui-liang-chong-fang-shi-de-/)
```c
class Solution {
public:
    int minDepth(TreeNode* root) {
        if (!root)  return 0;
        int left = minDepth(root->left);
        int right = minDepth(root->right);
        return (!root->left || !root->right) ? left + right + 1 : min(left, right) + 1;////如果有一个空，则+1,否则最小值+1
    }
};

```

***

