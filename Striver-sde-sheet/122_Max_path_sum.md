# Binary Tree Maximum Path Sum

## Problem statement

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

The **path sum** of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return the maximum **path sum** of any **non-empty** path.

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
int findMaxSum(TreeNode* root, int &res) {
    if(root == NULL) return 0;
    int l = max(0, findMaxSum(root->left, res));
    int r = max(0, findMaxSum(root->right, res));
    res = max(res, l + root->val + r);
    return root->val + max(l, r);
}
int maxPathSum(TreeNode* root) {
    int res = INT_MIN;
    findMaxSum(root, res);
    return res;
}
```
