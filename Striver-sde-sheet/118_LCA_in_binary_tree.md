# LCA in binary tree

## Problem statement

Given a binary tree, find the **lowest common ancestor** (LCA) of two given nodes in the tree.

The **lowest common ancestor** is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as **descendants** (where we allow a node to be a descendant of itself).

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if(root==NULL || root==p ||root==q) return root;
    TreeNode* left = lowestCommonAncestor(root->left, p, q);
    TreeNode* right = lowestCommonAncestor(root->right, p, q);
    if(!left) return right;
    if(!right) return left;
    return root;
}
```
