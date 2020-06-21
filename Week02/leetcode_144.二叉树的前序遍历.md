给定一个二叉树，返回它的 前序 遍历。

### c plus

***

* **递归法**
```c
class Solution {
public:
    vector<int> res;
    vector<int> preorderTraversal(TreeNode* root) {
        helper(root);
        return res;
    }
    void helper(TreeNode * root) {
        if (root == NULL) return;
        res.push_back(root->val);
        helper(root->left);
        helper(root->right);
    }
};

```

* **迭代法**
先访问根节点，即先将根节点存入结果，然后将右节点放入栈中，待访问完左子树后,右子树出栈访问。
```c
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        stack<TreeNode *>s;
        TreeNode *rt = root;
        while (rt || s.size())
        {
            while (rt) {
                res.push_back(rt->val);      
                s.push(rt->right);
                rt = rt->left;
            }
            rt = s.top();s.pop();
        }
        return res;
    }
};

```

***