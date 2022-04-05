# Symmetric binary tree

## Problem statement

Given the `root` of a binary tree, check whether it is a **mirror of itself** (i.e., symmetric around its center).

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
bool compare(TreeNode* root1, TreeNode* root2) {
    if(root1==NULL || root2==NULL) return root1==root2;
    if(root1->val != root2->val) return false;
    return compare(root1->left, root2->right) && compare(root1->right, root2->left);
}
bool isSymmetric(TreeNode* root) {
    return compare(root->left, root->right);
}
```
