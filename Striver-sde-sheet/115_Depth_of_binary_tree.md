# Maximum Depth of Binary Tree

## Problem statement

Given the `root` of a binary tree, return its **maximum depth**.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

## Solution

Time complexity : O(H)  
Auxiliary space : O(H)

```cpp
int maxDepth(TreeNode* root) {
    if(root == NULL) return 0;
    return 1 + max(maxDepth(root->left), maxDepth(root->right));
}
```
