给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

节点的左子树只包含小于当前节点的数。
节点的右子树只包含大于当前节点的数。
所有左子树和右子树自身必须也是二叉搜索树。

### c plus
***
* **利用中序遍历是升序的特征验证**
```c
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        TreeNode* prev = NULL;
        return inorder(root, prev);       //prev 是最前面的那个节点，如果是传值的话，这里应该传最小值。要保存节点指针供上一层使用，所以用指针引用。
    }
    bool inorder(TreeNode *root, TreeNode* &prev) {
        if (!root) return true;
        if(!inorder(root->left, prev)) return false;
        if (prev && (prev->val >= root->val)) return false;
        prev = root;
        return inorder(root->right, prev);
    }
};
```

* 根据定义判断
   
   [题解](https://leetcode-cn.com/problems/validate-binary-search-tree/solution/yi-zhang-tu-rang-ni-ming-bai-shang-xia-jie-zui-da-/)
```c
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return helper(root, LONG_MIN, LONG_MAX); 
    }
    bool helper(TreeNode *root, long long low, long long up) {
        if (!root) return true;
        if (root->val <= low || root->val >= up) return false;
        if (!helper(root->left, low, root->val)) return false;//左子树作为下个子树的上限
        return helper(root->right, root->val, up);//右子树作为下个子树的下限
    }
};

```

***