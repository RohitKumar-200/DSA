# Binary Tree Zigzag Level Order Traversal

## Problem statement

Given the `root` of a binary tree, return the **zigzag level order traversal** of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).

## Solution

Time complexity : O(N)  
Space compelxity : O(N)

```cpp
vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
    vector<vector<int>> res;
    if(root == NULL) return res;
    queue<TreeNode*> q;
    q.push(root);
    bool f = 1;
    while(!q.empty()) {
        int n = q.size();
        vector<int> v(n);
        for(int i=0; i<n; i++) {
            TreeNode* node = q.front();
            q.pop();
            int pos = f ? i : n-i-1;
            v[pos] = node->val;
            if(node->left) q.push(node->left);
            if(node->right) q.push(node->right);
        }
        res.push_back(v);
        f = !f;
    }
    return res;
}
```
