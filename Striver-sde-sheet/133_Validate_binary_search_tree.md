# Validate Binary Search Tree

## Problem statement

Given the `root` of a binary tree, determine if it is a **valid binary search tree** (BST).

## Solution 1 (validating range)

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
bool validateBST(TreeNode* root, long minVal, long maxVal) {
    if(root == NULL) return true;
    if(root->val <= minVal || root->val >= maxVal) return false;
    return validateBST(root->left, minVal, root->val)
        && validateBST(root->right, root->val, maxVal);
}
bool isValidBST(TreeNode* root) {
    return validateBST(root, LONG_MIN, LONG_MAX);
}
```

## Solution 2 (Inorder traversal)

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
bool validateBST(TreeNode* root, TreeNode* &prev) {
    if(root == NULL) return true;
    if(!validateBST(root->left, prev)) return false;
    if(prev!=NULL && prev->val >= root->val) return false;
    prev = root;
    return validateBST(root->right, prev);
}
bool isValidBST(TreeNode* root) {
    TreeNode* prev = NULL;
    return validateBST(root, prev);
}
```
