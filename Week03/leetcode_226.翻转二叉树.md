翻转一棵二叉树。
```
输入：                    
     4                
   /   \                 
  2     7                
 / \   / \                      
1   3 6   9     

输出：
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

### c plus
***

* **递归** 
   实质就是遍历二叉树，然后交换左右子树
   
    [题解](https://leetcode-cn.com/problems/invert-binary-tree/solution/dong-hua-yan-shi-liang-chong-shi-xian-226-fan-zhua/)
```c
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (root == NULL) return NULL;
        TreeNode *right = invertTree(root->right); //后序遍历，前序遍历先交换节点
        TreeNode *left = invertTree(root->left);  
        root->left = right;
        root->right = left;
        return root;
    }
};
```

* **迭代**
类似于广度优先遍历，层层扫荡，需要队列或栈来存储数据。
我们需要先将根节点放入到队列中，然后不断的迭代队列中的元素。
对当前元素调换其左右子树的位置，然后：
判断其左子树是否为空，不为空就放入队列中
判断其右子树是否为空，不为空就放入队列中
```c
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(root==NULL) return NULL;
        queue<TreeNode *> q;
        q.push(root);
        while (!q.empty()) {
            TreeNode *pre = q.front(); q.pop();
            TreeNode *tmp = pre->left;
            pre->left = pre->right;
            pre->right = tmp;
            if (pre->left != NULL)   q.push(pre->left);
            if (pre->right != NULL)  q.push(pre->right);
        } 
        return root;
    }
};
```

***