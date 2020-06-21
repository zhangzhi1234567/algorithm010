给定一个二叉树，返回它的中序 遍历。

### c plus
```c
 /**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
```
***
* 递归
```c
class Solution {
public:
    vector<int> res;
    vector<int> inorderTraversal(TreeNode* root) {
        helper(root);
        return res;
    }

    void helper(TreeNode* root) {
        if (root == NULL) return;
        helper(root->left);
        res.push_back(root->val);
        helper(root->right);
    }
     
};

```

* 迭代法

思路：每到一个节点 A，因为根的访问在中间，将 A 入栈。然后遍历左子树，接着访问 A，最后遍历右子树。
在访问完 A 后，A 就可以出栈了。因为 A 和其左子树都已经访问完成。
```
栈S;
p= root;
while(p || S不空){
    while(p){
        p入S;
        p = p的左子树;
    }
    p = S.top 出栈;
    访问p;
    p = p的右子树;
}
```
```c
class Solution {
public:
    
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        stack<TreeNode *> S;
        TreeNode* rt = root;
        while(rt || S.size()){
            while(rt){
                S.push(rt);
                rt=rt->left;
            }
            rt=S.top();S.pop();
            res.push_back(rt->val);
            rt=rt->right;
        }

        return res;
    }
};


```

***