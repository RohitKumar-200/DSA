# Binary Tree Level Order Traversal

## Problem statement

Given the `root` of a binary tree, return the **level order traversal** of its nodes' values. (i.e., from left to right, level by level).

## Solution

Time complexity : O(N)  
Space complexity : O(N)

```cpp
vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>> res;
    if(root == NULL) return res;
    queue<TreeNode*> q;
    q.push(root);
    while(!q.empty()) {
        vector<int> v;
        int sz = q.size();
        while(sz--) {
            TreeNode* node = q.front();
            q.pop();
            v.push_back(node->val);
            if(node->left) q.push(node->left);
            if(node->right) q.push(node->right);
        }
        res.push_back(v);
    }
    return res;
}
```
